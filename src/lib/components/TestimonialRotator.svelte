<script lang="ts">
import Testimonial from "#lib/components/Testimonial.svelte"
import { onMount } from "svelte"
const testimonials = [
  {
    content:
      "Lauren m’a apporté à la fois des connaissances, des solutions concrètes et beaucoup de confiance. Je lui suis profondément reconnaissante pour son accompagnement et je la recommande sans hésitation à toutes les mamans qui souhaitent être accompagnées dans leur allaitement avec expertise, douceur et humanité.",
    author: { name: "Andreea" },
  },
  {
    content:
      "Lauren est une professionnelle très qualifiée. Elle est douce, à l’écoute et bienveillante. Notre consultation s’est très bien passé, elle a prit le temps de répondre à toutes mes interrogations, m’a donné de précieux conseils avec beaucoup de douceurs et sans aucun jugement. Je me suis sentie écoutée, comprise et rassurée. Un accompagnement de qualité merci.",
    author: { name: "Chloé" },
  },
  {
    content:
      "Lauren m’a accompagné durant mon allaitement, ayant eu une réduction mammaire j’avais des doutes sur la possibilité d’allaiter et cela a fonctionné grâce à tous ses conseils et son accompagnement. Elle est bienveillante et investie pour répondre au mieux à nos demandes. Je la recommande à 100%.",
    author: { name: "Alexia" },
  },
  {
    content:
      "Merci Lauren pour cette consultation, j’ai adoré cet échange. Votre douceur et votre bienveillance permet de se sentir en confiance et à l’écoute. Et merci encore pour tous vos précieux conseils ! C’est pour moi une belle rencontre.",
    author: { name: "Magali" },
  },
  {
    content:
      "Consultation très instructive auprès de Lauren quant à mon allaitement en cours. Elle a su répondre avec clarté et précision à toutes mes questions, à travers une approche rassurante et bienveillante. Je la recommande les yeux fermés.",
    author: { name: "Mallorie" },
  },
]

let rotator: HTMLDivElement
let perPage = $state(3)
let currentPage = $state(0)
let pageCount = $derived(Math.ceil(testimonials.length / perPage))
let announcement = $derived.by(() => {
  const first = Math.min(currentPage * perPage, testimonials.length - perPage)
  if (perPage === 1) {
    return `Témoignage ${first + 1} sur ${testimonials.length}, ${
      testimonials[first].author.name
    }`
  }
  return `Témoignages ${first + 1} à ${
    Math.min(first + perPage, testimonials.length)
  } sur ${testimonials.length}`
})

function pageWidth() {
  const first = rotator.children[0] as HTMLElement
  const second = rotator.children[1] as HTMLElement
  return (second.offsetLeft - first.offsetLeft) * perPage
}

function updatePosition() {
  if (rotator.scrollLeft >= rotator.scrollWidth - rotator.clientWidth - 1) {
    currentPage = pageCount - 1
    return
  }
  currentPage = Math.min(
    pageCount - 1,
    Math.round(rotator.scrollLeft / pageWidth()),
  )
}

function updateLayout() {
  perPage = matchMedia("(max-width: 1023px)").matches ? 1 : 3
  updatePosition()
}

function goTo(page: number) {
  rotator.scrollTo({
    left: Math.max(0, Math.min(pageCount - 1, page)) * pageWidth(),
    behavior: matchMedia("(prefers-reduced-motion: reduce)").matches
      ? "instant"
      : "smooth",
  })
}

onMount(updateLayout)
</script>

<svelte:window onresize={updateLayout} />

<div class="testimonials-rotator" role="region"
  aria-roledescription="carrousel"
  aria-label="Témoignages">
  <div class="testimonials-track" bind:this={rotator} onscroll={updatePosition}
    aria-label="Témoignages à faire défiler">
    {#each testimonials as testimonial, index (testimonial)}
      <Testimonial {...testimonial} position={index + 1} total={testimonials.length} />
    {/each}
  </div>
  <p class="rotator-announcement" aria-live="polite" aria-atomic="true">{announcement}</p>
  {#if pageCount > 1}
    <div class="testimonials-controls">
    <button class="testimonials-arrow" type="button"
      onclick={() => goTo(currentPage - 1)}
      aria-label="Témoignages précédents">
      <svg aria-hidden="true" width="20" height="20" viewBox="0 0 24 24"
        fill="none" stroke="currentColor" stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round">
        <path d="m15 18-6-6 6-6"></path>
      </svg>
    </button>
    <div class="testimonials-dots" role="group"
      aria-label="Choisir une page de témoignages">
      {#each Array(pageCount) as _, index (index)}
        <button class="testimonials-dot" type="button" onclick={() => goTo(index)}
          aria-label={`Page ${index + 1} sur ${pageCount}`}
          aria-current={currentPage === index ? "true" : undefined}></button>
      {/each}
    </div>
    <button class="testimonials-arrow" type="button"
      onclick={() => goTo(currentPage + 1)}
      aria-label="Témoignages suivants">
      <svg aria-hidden="true" width="20" height="20" viewBox="0 0 24 24"
        fill="none" stroke="currentColor" stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round">
        <path d="m9 18 6-6-6-6"></path>
      </svg>
    </button>
    </div>
  {/if}
</div>

<style>
.rotator-announcement {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip-path: inset(50%);
  white-space: nowrap;
  border: 0;
}
.testimonials-rotator {
  margin-top: 48px;
}
.testimonials-track {
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: calc((100% - 32px) / 3);
  gap: 16px;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
}
.testimonials-track::-webkit-scrollbar {
  display: none;
}
.testimonials-controls {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 16px;
}
.testimonials-controls .testimonials-arrow {
  width: 44px;
  height: 44px;
  display: grid;
  place-items: center;
  padding: 0;
  border: 0;
  background: transparent;
  color: var(--deep);
  cursor: pointer;
}
.testimonials-controls .testimonials-arrow:hover {
  color: var(--terracotta);
}
.testimonials-dots {
  display: flex;
  align-items: center;
}
.testimonials-dot {
  display: grid;
  place-items: center;
  width: 24px;
  height: 44px;
  padding: 0;
  border: 0;
  background: transparent;
  cursor: pointer;
}
.testimonials-dot::before {
  content: "";
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--deep);
  opacity: 0.3;
}
.testimonials-dot[aria-current="true"]::before {
  opacity: 1;
}
@media (max-width: 1023px) {
  .testimonials-track {
    grid-auto-columns: 100%;
  }
}
</style>
