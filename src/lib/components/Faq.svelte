<script lang="ts">
const questions = [
  {
    question: "Où a lieu la consultation ?",
    answer:
      "À Dijon au centre ville, au cabinet, à votre domicile dans un rayon de 20 km ou encore en visio.",
  },
  {
    question: "Comment se déroule la consultation, combien de temps ça dure ?",
    answer:
      "Pendant environ 1 heure je prends le temps de comprendre ton projet, tes envies, de déceler tes craintes. Si tu ne t'y opposes pas, je procède à une analyse clinique des seins. Si tu es en cours d'allaitement, j'analyse une tétée, t'en fais un retour et ajuste en fonction. Je réalise systématiquement la courbe de poids de ton bébé et t'en fais un retour également.",
  },
  {
    question:
      "J'ai eu une chirurgie sur mes seins (prothèse, diminution) pourrais-je allaiter ?",
    answer:
      "Avec une réduction mammaire ou une augmentation, il est possible d'allaiter mais chaque femme est différente, viens me parler de ton projet (avec ton compte rendu opératoire) et je t'aiderai dans la pratique.",
  },
  {
    question: "Comment préparer mon allaitement pendant la grossesse ?",
    answer:
      "Une consultation prénatale permet de comprendre le fonctionnement de la lactation, de savoir à quoi s'attendre les premiers jours, de repérer les situations qui demandent une vigilance particulière et de préparer ton entourage.",
  },
  {
    question: "Quelles sont les bonnes positions pour allaiter ?",
    answer:
      "La bonne position sera la tienne, celle qui te conviendra et qui sera efficace, zéro douleur, une maman confortable et un bébé qui reçoit des quantités de lait suffisantes.",
  },
  {
    question: "Peut-on produire une quantité insuffisante de lait ?",
    answer:
      "En fonction de la conduite d'allaitement il est possible que la quantité ne soit pas optimale, en général cela se traduit sur la courbe de croissance, un bébé qui pleure beaucoup, ou au contraire qui dort beaucoup ou alors un bébé qui passe sa journée au sein.",
  },
  {
    question: "Et si on me pousse à donner un biberon à la maternité ?",
    answer:
      "Parfois il arrive qu'il faille donner un complément à ton bébé, mais pourquoi pas un complément de lait maternel, le tien, pour cela vient me parler de ta situation nous pourrons appréhender les différents scénarii.",
  },
  {
    question:
      "Si j'accouche par césarienne, comment faire pour démarrer mon allaitement ?",
    answer:
      "Cela dépendra de l'établissement dans lequel vous allez accoucher, tous les protocoles ne sont pas uniformisés, mais si tu peux maîtriser l'expression manuelle du colostrum c'est déjà un plus.",
  },
  {
    question: "Je pense que mon bébé a un frein de langue, que faire ?",
    answer:
      "C'est possible, mais cela gène t il la prise du sein et la tétée ? Vient faire le point en consultation.",
  },
  {
    question: "Comment savoir si mon bébé prend assez de lait ?",
    answer:
      "On peut aisément s'en rendre compte en fonction du nombre de couches qu'il mouille par 24h en fonction de son âge. Après les premiers jours, un bébé qui boit suffisamment fait régulièrement des selles et des urines abondantes, tète activement avec des déglutitions audibles, et reprend du poids après la perte initiale physiologique. Des tétées fréquentes, y compris la nuit, sont normales et ne signifient pas à elles seules un manque de lait. En cas de doute, une consultation permet de faire le point.",
  },
  {
    question: "Mon bébé tète tout le temps, ai-je assez de lait ?",
    answer:
      "Le nouveau né est naturellement programmé pour téter. Parfois, lorsque le transfert de lait n'est pas optimal, que la tétée n'est donc pas assez efficace, c'est possible que le nouveau né soit \"constamment au sein\". Ces situations sont souvent épuisantes pour la maman, mais heureusement il y a des remèdes à ce comportement.",
  },
  {
    question: "Pourquoi ai-je des crevasses ?",
    answer:
      "Les crevasses sont souvent dues à une mauvaise prise du sein en bouche par le bébé ou encore à un tire-lait mail utilisé ou encore à une infection en cours, viens faire le point sur ta situation.",
  },
  {
    question: "Comment utiliser un tire-lait ?",
    answer:
      "Plusieurs tailles de téterelles existent sur le marché en fonction du modèle de tire lait que tu utilises, la téterelle ne doit pas te blesser et les fréquences de tirage sont à adapter en fonction de ta situation.",
  },
  {
    question: "Puis-je continuer à allaiter en reprenant le travail ?",
    answer:
      "Oui, c'est tout à fait possible. Selon ton organisation et l'allaitement en cours, nous construisons ensemble un plan réaliste, adapté à ton rythme et à ton mode de garde.",
  },
  {
    question: "J'ai mal quand mon bébé prend mon sein est ce normal ?",
    answer:
      "On peut ressentir une sensibilité les premiers jours (cause hormonale), mais une douleur vive qui persiste tout au long de la tétée ou des crevasses ne sont pas normales. Elles viennent souvent d'une position ou d'une prise du sein à ajuster, ce qui se corrige généralement bien. N'attends pas que la douleur s'installe : plus on agit tôt, plus c'est simple.",
  },
  {
    question:
      "Je voudrais faire participer le papa dans l'allaitement, comment faire ?",
    answer:
      "Allaiter demande à la maman une grande disponibilité et papa ou le co-parent n'est pas là uniquement pour changer les couches. Une maman apprécie toujours que le papa se rende disponible pour bercer bébé, libérer la maman pour qu'elle aille prendre une douche, faire une sieste.",
  },
  {
    question:
      "Mon bébé n’arrive pas à prendre le sein, il s'énerve, que faire ?",
    answer:
      "Il arrive que certaines mises au sein soient compliquées, bébé pleure, ouvre la bouche mais ne tète pas, ne s'accroche pas. Pour plus de facilités, je t'oriente vers une mise au sein dès que le bébé est prêt à téter, c'est-à-dire en sommeil actif.",
  },
]
</script>

<section class="section faq" id="faq" aria-labelledby="faq-title">
  <h2 id="faq-title">Questions fréquentes</h2>
  <div class="faq-items">
    {#each questions as item (item.question)}
      <details>
        <summary>
          <span class="faq-icon" aria-hidden="true"></span>
          <span>{item.question}</span>
        </summary>
        <p>{item.answer}</p>
      </details>
    {/each}
  </div>
</section>

<style>
.faq {
  background: var(--cream);
}

.faq-items {
  margin: 40px auto 0;
  border-top: 1px solid var(--line);
}

details {
  border-bottom: 1px solid var(--line);
}

summary {
  display: flex;
  align-items: baseline;
  gap: 12px;
  list-style: none;
  padding: 24px 4px;
  cursor: pointer;
  font-weight: 600;
  line-height: 1.5;
}

summary::-webkit-details-marker {
  display: none;
}

.faq-icon {
  flex: 0 0 1em;
  color: var(--terracotta);
  text-align: center;
}

.faq-icon::before {
  content: "+";
}

details[open] .faq-icon::before {
  content: "−";
}

summary:hover {
  color: var(--terracotta);
}

summary:focus-visible {
  outline: 3px solid var(--terracotta);
  outline-offset: 4px;
}

details p {
  margin: 0;
  padding: 0 4px 24px;
  color: var(--muted);
}
</style>
