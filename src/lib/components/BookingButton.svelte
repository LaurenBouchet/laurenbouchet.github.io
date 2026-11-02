<script lang="ts">
import { site } from "#lib/config.ts"

let { inverse = false }: { inverse?: boolean } = $props()
</script>

{#if site.bookingUrl}
  <!-- The booking URL points to an external service. -->
  <a class:inverse class="booking-button" href={site.bookingUrl} target="_blank"
  rel="noreferrer">
  <span class="booking-label">Prendre rendez‑vous</span>
  <span aria-hidden="true">↗</span>
</a>
{:else}
  <button class:inverse class="booking-button" disabled>
  <span class="booking-label">Prendre rendez‑vous</span>
  <span aria-hidden="true">↗</span>
</button>
{/if}
