<script lang="ts">
  import { page } from "$app/state"
  import "../app.css"

  let { children } = $props()
</script>

{#key page.url.pathname}
  <div class="page-enter">
    {@render children()}
  </div>
{/key}
