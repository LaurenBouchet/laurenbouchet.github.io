<script lang="ts">
  import BookingButton from "$lib/components/BookingButton.svelte"
  import Header from "$lib/components/Header.svelte"
  import Head from "$lib/components/Head.svelte"

  const concerns = [
    "Douleurs pendant l’allaitement",
    "Prise de poids insuffisante",
    "Perte de poids du bébé",
    "Bébé qui ne tète pas",
    "Baisse de lactation",
    "Coliques",
    "Reprise du travail",
    "Réduction mammaire",
    "Diversification alimentaire",
    "Sevrage",
    "Utilisation du tire-allaitement",
  ]
</script>

<Head />

<div class="site-shell">
  <Header />

  <main>
    <section class="hero" id="accompagnements" aria-labelledby="hero-title">
      <div class="hero-copy">
        <h1 id="hero-title">
          Être accompagnée dans votre allaitement, avant et après la naissance
        </h1>
        <p class="intro">
          Que vous soyez en train d’imaginer votre allaitement avant l’arrivée de bébé, que vous
          sortiez de la maternité ou que vous rencontriez une difficulté (douleur, prise de poids
          insuffisante, baisse de lactation, colique ou pleur du nourrisson, réduction mammaire,
          diversification alimentaire, reprise du travail, tire-allaitement, sevrage) vous trouverez
          dans la consultation un plan d’action pensé pour vous et votre bébé, à votre rythme.
        </p>
      </div>
      <div class="hero-visual" aria-hidden="true">
        <div class="portrait-placeholder">
          <span aria-hidden="true">✦</span>
        </div>
      </div>
      <div class="hero-services">
        <div class="service-grid">
          <article class="service-card">
            <h3>Préparer votre allaitement</h3>
            <p>
              Avant la naissance, prenez le temps de poser vos questions et de préparer les
              premières tétées avec confiance.
            </p>
            <ul>
              <li>Mieux appréhender votre projet d’allaitement</li>
              <li>Mieux comprendre votre corps pour accueillir le bébé</li>
            </ul>
          </article>
          <article class="service-card">
            <h3>Pendant l’allaitement</h3>
            <p>
              Des réponses concrètes aux difficultés rencontrées et aux nouvelles étapes à préparer.
            </p>
            <ul class="concern-list">
              {#each concerns as concern (concern)}<li>{concern}</li>{/each}
            </ul>
          </article>
        </div>
      </div>
    </section>

    <section class="section format" aria-labelledby="format-title">
      <h2 id="format-title">Où je vous accompagne</h2>
      <div class="format-items">
        <article>
          <div class="format-image" aria-hidden="true"></div>
          <h3>À Dijon, et ses alentours</h3>
          <p>Dans un rayon d’environ 30 km.</p>
        </article>
        <article>
          <div class="format-image" aria-hidden="true"></div>
          <h3>En visioconférence</h3>
          <p>Via Whatsapp ou autre</p>
        </article>
      </div>
    </section>

    <section class="section pricing" id="tarifs" aria-labelledby="pricing-title">
      <div class="section-heading"><h2 id="pricing-title">Mes tarifs</h2></div>
      <div class="table-wrap">
        <table>
          <thead><tr><th scope="col">Consultation</th><th scope="col">Tarif</th></tr></thead>
          <tbody>
            <tr>
              <td>
                <strong>Consultation allaitement — 1er rendez-vous</strong>
                <p>
                  Pour préparer votre allaitement ou poser toute question sur votre allaitement en
                  cours.
                </p>
              </td>
              <td>40 €</td>
            </tr>
            <tr>
              <td>
                <strong>Consultation de suivi</strong>
                <p>Réservée aux patientes déjà suivies.</p>
              </td>
              <td>30 €</td>
            </tr>
            <tr>
              <td>
                <strong>SOS consultation allaitement</strong>
                <p>Une réponse rapide dans la journée pour les situations urgentes, 7 j/7.</p>
              </td>
              <td>35 €</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <section class="section reviews" aria-labelledby="reviews-title">
      <div class="review-content">
        <h2 id="reviews-title">Le retour d’Andreea</h2>
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

    <section class="cta-section" id="rendez-vous" aria-labelledby="cta-title">
      <h2 id="cta-title">Faisons le point sur votre allaitement</h2>
      <BookingButton inverse={true} />
    </section>
  </main>
  <footer class="site-footer">Lauren Bouchet © Tous droits réservés</footer>
</div>
