<script lang="ts">
let { status = 404 }: { status?: number } = $props()
</script>

<svelte:head>
  <title>{status === 404 ? "Page introuvable" : "Une erreur est survenue"} — Lauren Bouchet</title>
  <meta name="robots" content="noindex" />
</svelte:head>

<div class="error-shell">
  <header class="error-header">
    <a class="brand" href="/" aria-label="Lauren Bouchet, accueil">
      <span class="brand-mark" aria-hidden="true">L</span>
      <span><strong>Lauren Bouchet</strong><small>Consultante en allaitement</small></span>
    </a>
  </header>

  <main class="error-main">
    <div class="error-content">
      <p
        class="eyebrow">{status === 404 ? "Erreur 404" : `Erreur ${status}`}</p>
      <h1
        class:single-line={status === 404}>{status === 404 ? "Vous êtes perdu ?" : "Une petite difficulté est survenue"}</h1>
      <p class="error-description">
        {status === 404
          ? "La page que vous cherchez n’existe pas ou a changé d’adresse. Retrouvons le chemin ensemble."
          : "La page ne peut pas être affichée pour le moment. Vous pouvez revenir à l’accueil et réessayer."}
      </p>
      <a class="booking-button"
        href="/">Retour à l’accueil <span aria-hidden="true">→</span></a>
    </div>
  </main>

  <footer class="site-footer">Lauren Bouchet © Tous droits réservés</footer>
</div>

<style>
.error-shell {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.error-header {
  flex-shrink: 0;
}
.error-main {
  flex: 1;
  display: grid;
  place-items: center;
  padding: 80px var(--gutter);
  background: var(--cream);
}
.error-content {
  max-width: 580px;
  text-align: center;
}
.error-content h1 {
  margin: 0 auto 28px;
}
.error-content h1.single-line {
  font-size: clamp(2rem, 6vw, 4.5rem);
  white-space: nowrap;
}
.error-description {
  max-width: 470px;
  margin: 0 auto 32px;
  color: var(--muted);
  font-size: 1.12rem;
}
@media (max-width: 800px) {
  .error-main {
    padding: 64px 20px;
  }
}
</style>
