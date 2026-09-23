<script lang="ts">
  import { site } from "$lib/config"

  let { inverse = false }: { inverse?: boolean } = $props()
</script>

{#if site.bookingUrl}
  <!-- The booking URL points to an external service. -->
  <!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
  <a class:inverse class="booking-button" href={site.bookingUrl} target="_blank" rel="noreferrer">
    Prendre rendez‑vous
    <span aria-hidden="true">↗</span>
  </a>
{:else}
  <button class:inverse class="booking-button" disabled>
    Prendre rendez‑vous
    <span aria-hidden="true">↗</span>
  </button>
{/if}
