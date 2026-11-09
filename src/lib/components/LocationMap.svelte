<script lang="ts">
import { onMount } from "svelte"
import type { Map as MapLibreMap } from "maplibre-gl"
import "maplibre-gl/dist/maplibre-gl.css"
import workerUrl from "maplibre-gl/dist/maplibre-gl-worker.mjs?worker&url"

let { showRadius = false }: { showRadius?: boolean } = $props()
const center: [number, number] = [5.046676, 47.325949]
const radiusRadians = 20 / 6371
const latitude = center[1] * Math.PI / 180
const longitude = center[0] * Math.PI / 180
const coordinates = Array.from({ length: 129 }, (_, index) => {
  const bearing = 2 * Math.PI * index / 128
  const lat = Math.asin(
    Math.sin(latitude) * Math.cos(radiusRadians) +
      Math.cos(latitude) * Math.sin(radiusRadians) * Math.cos(bearing),
  )
  const lon = longitude + Math.atan2(
    Math.sin(bearing) * Math.sin(radiusRadians) * Math.cos(latitude),
    Math.cos(radiusRadians) - Math.sin(latitude) * Math.sin(lat),
  )
  return [lon * 180 / Math.PI, lat * 180 / Math.PI]
})
coordinates[128] = coordinates[0]
const longitudes = coordinates.map((point) => point[0])
const latitudes = coordinates.map((point) => point[1])
const bounds: [[number, number], [number, number]] = [
  [Math.min(...longitudes), Math.min(...latitudes)],
  [Math.max(...longitudes), Math.max(...latitudes)],
]

let container: HTMLDivElement
let mapReady = $state(false)
let map: MapLibreMap | undefined

function recenter(duration = 800) {
  if (showRadius) {
    map?.fitBounds(bounds, { padding: 30, duration })
  } else {
    map?.easeTo({ center, zoom: 14, duration })
  }
}

onMount(() => {
  let disposed = false
  const observer = new IntersectionObserver(async (entries) => {
    if (!entries.some((entry) => entry.isIntersecting)) return
    observer.disconnect()

    try {
      const {
        AttributionControl,
        Map,
        Marker,
        NavigationControl,
        setWorkerUrl,
      } = await import("maplibre-gl")
      if (disposed) return
      setWorkerUrl(workerUrl)
      map = new Map({
        container,
        style: "https://tiles.openfreemap.org/styles/liberty",
        center,
        zoom: showRadius ? 9 : 14,
        interactive: false,
        attributionControl: false,
      })
      map.addControl(new AttributionControl({ compact: true }), "bottom-right")
      map.addControl(new NavigationControl({ showCompass: false }), "top-right")
      if (!showRadius) {
        new Marker({ color: "#8b4637" }).setLngLat(center).addTo(map)
      }

      map.on("load", () => {
        if (!map) return
        const attribution = container.querySelector<HTMLDetailsElement>(
          ".maplibregl-ctrl-attrib",
        )
        attribution?.removeAttribute("open")
        attribution?.classList.remove("maplibregl-compact-show")
        mapReady = true
        const fills: Record<string, string> = {
          park: "#e5e5d2",
          landuse_residential: "#f2e8dc",
          landcover_wood: "#dedfc9",
          landcover_grass: "#e8e8d8",
          water: "#d5e2df",
          building: "#e3d1c1",
        }
        for (const [id, color] of Object.entries(fills)) {
          if (map.getLayer(id)) map.setPaintProperty(id, "fill-color", color)
        }
        if (map.getLayer("background")) {
          map.setPaintProperty("background", "background-color", "#f7f0e7")
        }
        if (showRadius) {
          map.addSource("service-area", {
            type: "geojson",
            data: {
              type: "Feature",
              properties: {},
              geometry: { type: "Polygon", coordinates: [coordinates] },
            },
          })
          map.addLayer({
            id: "service-area-fill",
            type: "fill",
            source: "service-area",
            paint: { "fill-color": "#8b4637", "fill-opacity": 0.15 },
          })
          map.addLayer({
            id: "service-area-outline",
            type: "line",
            source: "service-area",
            paint: { "line-color": "#8b4637", "line-width": 2 },
          })
          recenter(0)
        }
      })
    } catch {
      // Leave the placeholder visible if the map cannot initialize.
    }
  }, { rootMargin: "200px" })

  observer.observe(container)
  return () => {
    disposed = true
    observer.disconnect()
    map?.remove()
  }
})
</script>

<div class="format-image format-map" class:map-ready={mapReady}>
  <div class="format-map-canvas" bind:this={container} role="region"
    aria-label={showRadius ? "Carte de la zone d’intervention de 20 km autour du cabinet" : "Carte du cabinet à Dijon"}></div>
  {#if mapReady}
    <button class="map-recenter" type="button" aria-label="Recentrer la carte"
      title="Recentrer la carte"
      onclick={() => recenter()}>
      <svg aria-hidden="true" width="16" height="16" viewBox="0 0 24 24"
        fill="none" stroke="currentColor" stroke-width="2.8">
        <circle cx="12" cy="12" r="6"></circle>
        <path d="M12 2v4m0 12v4M2 12h4m12 0h4"></path>
      </svg>
    </button>
  {/if}
</div>
