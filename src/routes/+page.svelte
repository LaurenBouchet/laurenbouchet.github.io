<script lang="ts">
import BookingButton from "#lib/components/BookingButton.svelte"
import Header from "#lib/components/Header.svelte"
import Head from "#lib/components/Head.svelte"
import Faq from "#lib/components/Faq.svelte"
import ConstructionBanner from "#lib/components/ConstructionBanner.svelte"
import LocationMap from "#lib/components/LocationMap.svelte"

const cabinetMapUrl =
  "https://www.openstreetmap.org/?mlat=47.325949&mlon=5.046676#map=17/47.325949/5.046676"

function openCabinetMap(event: MouseEvent) {
  if (event.metaKey || event.ctrlKey || event.shiftKey || event.altKey) return
  const isAndroid = /Android/i.test(navigator.userAgent)
  const isAppleMobile = /iPhone|iPad|iPod/i.test(navigator.userAgent) ||
    (navigator.platform === "MacIntel" && navigator.maxTouchPoints > 1)
  if (!isAndroid && !isAppleMobile) return

  event.preventDefault()
  const address = encodeURIComponent("3 boulevard Thiers, 21000 Dijon")
  const appUrl = isAndroid
    ? `geo:47.325949,5.046676?q=${address}`
    : `maps://?ll=47.325949,5.046676&q=${address}`
  window.location.href = appUrl
}

const supportPrinciples = [
  {
    title: "Écouter d’abord",
    description:
      "Votre histoire, votre bébé et vos envies comptent plus que n’importe quelle règle.",
  },
  {
    title: "Observer ensemble",
    description:
      "Position, mise au sein, tétées : nous regardons concrètement ce qui se passe, au calme.",
  },
  {
    title: "Respecter vos choix",
    description:
      "Mon rôle est de vous donner des repères clairs pour que vous décidiez en confiance, pas de vous imposer une méthode.",
  },
  {
    title: "Vous soutenir dans la durée",
    description:
      "Je reste disponible après la consultation pour ajuster, rassurer et suivre l’évolution.",
  },
]
</script>

<Head />

<div class="site-shell">
  <ConstructionBanner />
  <Header />

  <main>
    <section class="hero" id="accompagnements" aria-labelledby="hero-title">
      <div class="hero-copy">
        <h1 id="hero-title">L’allaitement, une étape dans nos vies</h1>
        <p class="intro">
          Vous attendez un bébé, ou il est déjà là. Et vous vous posez mille questions sur
          l’allaitement. Peut-être avez-vous entendu tout et son contraire, ou eu le sentiment de ne
          pas être vraiment écoutée. Peut-être est-ce douloureux, vous demandez-vous si bébé prend
          assez de poids ? Ici, vous pouvez poser votre fatigue, vos doutes et vos questions, sans
          jugement.
        </p>
        <div class="hero-visual hero-visual-mobile" aria-hidden="true">
          <div class="portrait-placeholder">
            <span aria-hidden="true">✦</span>
          </div>
        </div>
        <p class="intro">
          Je m’appelle Lauren, je suis infirmière puéricultrice diplômée d’État et je me forme
          actuellement à la certification IBCLC. Je travaille en néonatologie auprès des tout-petits
          et des mamans, et j’accompagne des familles dans ces premiers jours où tout bascule. J’ai
          aussi allaité mes deux enfants, sans jamais trouver un accompagnement serein. Je sais que
          l’allaitement est beau, mais qu’il peut aussi être exigeant, et que personne ne devrait le
          traverser seule.
        </p>
      </div>
      <div class="hero-visual hero-visual-desktop" aria-hidden="true">
        <div class="portrait-placeholder">
          <span aria-hidden="true">✦</span>
        </div>
      </div>
      <div class="hero-services">
        <div class="service-grid">
          <article class="service-card">
            <h3>Vous attendez un bébé et souhaitez allaiter ?</h3>
            <p>
              Premier allaitement, expérience précédente difficile, projet de tire-allaitement,
              antécédent de chirurgie mammaire (augmentation ou réduction) : je vous donne des
              repères clairs pour aborder votre projet avec confiance.
            </p>
          </article>
          <article class="service-card">
            <h3>Vous avez accouché et rencontrez des difficultés ?</h3>
            <p>
              Douleurs, crevasses, prise de poids insuffisante, pleurs de votre bébé… Vous n’avez pas
              à traverser ces premiers jours seule. Je suis là pour vous écouter, observer avec vous
              et trouver des solutions adaptées.
            </p>
          </article>
          <article class="service-card">
            <h3>Vous reprenez bientôt le travail ?</h3>
            <p>
              Utilisation du tire-lait, organisation des tétées, diversification alimentaire :
              prenez rendez-vous pour en parler ensemble et préparer cette transition sereinement.
            </p>
          </article>
        </div>
      </div>
    </section>

    <section class="section approach" aria-labelledby="approach-title">
      <div class="section-heading">
        <h2 id="approach-title">Ma façon de vous accompagner</h2>
      </div>
      <div class="approach-grid">
        {#each supportPrinciples as principle, index (principle.title)}
          <article>
            <h3><span class="approach-number">{index + 1}.</span> {principle.title}</h3>
            <p>{principle.description}</p>
          </article>
        {/each}
      </div>
    </section>

    <section class="section format" aria-labelledby="format-title">
      <h2 id="format-title">Où se retrouver</h2>
      <div class="format-items">
        <article>
          <a class="location-link"
            href={cabinetMapUrl} target="_blank" rel="noopener noreferrer"
            onclick={openCabinetMap}>
            <h3>À mon cabinet</h3>
            <p>3 boulevard Thiers, 21000 Dijon</p>
          </a>
          <LocationMap />
        </article>
        <article>
          <h3>À votre domicile</h3>
          <p>À Dijon et dans un rayon de 20 km.</p>
          <LocationMap showRadius={true} />
        </article>
        <article>
          <h3>En visioconférence</h3>
          <p>Via Whatsapp ou autre</p>
          <div class="format-image" aria-hidden="true"></div>
        </article>
      </div>
    </section>

    <section class="section pricing" id="tarifs"
      aria-labelledby="pricing-title">
      <div class="section-heading">
        <h2 id="pricing-title">Mes tarifs</h2>
      </div>
      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th scope="col">Consultation</th>
              <th scope="col">Temps · Tarif</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <strong>Consultation allaitement - 1er rendez-vous</strong>
                <p>
                  Pour préparer votre allaitement ou poser toute question sur votre allaitement en
                  cours.
                </p>
              </td>
              <td>60 min · 50 €</td>
            </tr>
            <tr>
              <td>
                <strong>Consultation de suivi - Réservé aux patientes déjà suivies</strong>
              </td>
              <td>45 min · 40 €</td>
            </tr>
            <tr>
              <td>
                <strong>SOS allaitement</strong>
                <p>Une réponse rapide dans la journée pour les situations urgentes, 7j/7.</p>
              </td>
              <td>30 min · 60 €</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <section class="section reviews" aria-labelledby="reviews-title">
      <div class="review-content">
        <h2 id="reviews-title">Témoigniage</h2>
        <figure>
          <blockquote>
            <p>
              « Lauren m’a accompagnée pendant les premières semaines de mon allaitement, une
              période aussi merveilleuse qu’intense, où l’on peut rapidement se retrouver avec
              beaucoup de questions, de doutes et d’émotions.
            </p>
            <p>
              Ce que j’ai particulièrement apprécié chez Lauren, c’est la combinaison assez rare
              entre une véritable expertise de l’allaitement et une très grande qualité d’écoute.
              Elle maîtrise parfaitement les aspects techniques — positionnement, prise du sein,
              rythme des tétées, lactation, petits ajustements du quotidien — mais elle sait surtout
              observer, écouter et comprendre ce dont une maman a besoin à un moment donné.
            </p>
            <p>
              Lauren a été extrêmement attentive aux détails et très proactive. Elle ne se
              contentait pas de répondre à mes questions&nbsp;: elle observait, anticipait certaines
              difficultés et me proposait des solutions très concrètes et adaptées à ma situation.
              J’ai également beaucoup apprécié sa capacité à comprendre mes états d’esprit, à sentir
              les moments où j’avais besoin d’être rassurée, encouragée ou simplement écoutée,
              toujours avec beaucoup de douceur et sans jamais être intrusive.
            </p>
            <p>
              Dans ces premières semaines où l’on apprend à connaître son bébé tout en prenant
              confiance dans son propre rôle de maman, avoir à ses côtés quelqu’un d’aussi
              compétent, bienveillant et attentif fait une vraie différence.
            </p>
            <p>
              Lauren m’a apporté à la fois des connaissances, des solutions concrètes et beaucoup de
              confiance. Je lui suis profondément reconnaissante pour son accompagnement et je la
              recommande sans hésitation à toutes les mamans qui souhaitent être accompagnées dans
              leur allaitement avec expertise, douceur et humanité. »
            </p>
          </blockquote>
          <figcaption>Andreea</figcaption>
        </figure>
      </div>
    </section>

    <Faq />

    <section class="cta-section" id="rendez-vous" aria-labelledby="cta-title">
      <h2 id="cta-title">Faisons le point sur votre allaitement</h2>
      <BookingButton inverse={true} />
    </section>
  </main>
  <footer class="site-footer">Lauren Bouchet © Tous droits réservés</footer>
</div>
