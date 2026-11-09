<script lang="ts">
let { content, author, position, total }: {
  content: string
  author: { name: string }
  position: number
  total: number
} = $props()

let textScale = $derived(
  1 + 0.3 * Math.min(1, Math.max(0, (300 - content.length) / 220)),
)
</script>

<figure class="testimonial-card" role="group" aria-roledescription="témoignage"
  aria-label={`${position} sur ${total}`}
  style:--testimonial-text-scale={textScale}>
  <blockquote>« {content} »</blockquote>
  <figcaption>— {author.name}</figcaption>
</figure>

<style>
.testimonial-card {
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 28px;
  background: var(--paper);
  border: 1px solid var(--line);
  border-radius: 16px;
  scroll-snap-align: start;
}
blockquote {
  display: flex;
  align-items: center;
  flex: 1;
  margin: 0;
  color: var(--ink);
  font: 1.16rem/1.75 Georgia, "Times New Roman", serif;
  font-size: calc(1.16rem * var(--testimonial-text-scale));
  white-space: pre-line;
}
figcaption {
  margin-top: 24px;
  color: var(--terracotta);
  font-size: 1rem;
  font-weight: 700;
  text-align: right;
}
@media (max-width: 800px) {
  .testimonial-card {
    border-radius: 12px;
  }
  blockquote {
    font-size: calc(1rem * var(--testimonial-text-scale));
    line-height: 1.6;
  }
}
</style>
