<script lang="ts">
let { content, author, position, total }: {
  content: string
  author: { name: string; avartarUrl: string }
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
  <figcaption>
    <span class="testimonial-avatar" aria-hidden="true">
      <img src={author.avartarUrl} alt="" />
    </span>
    <span>{author.name}</span>
  </figcaption>
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
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  margin-top: 32px;
  padding-top: 20px;
  border-top: 1px solid var(--line);
  color: var(--terracotta);
  font-size: 1rem;
  font-weight: 700;
  text-align: right;
}
.testimonial-avatar {
  display: grid;
  flex: 0 0 48px;
  width: 48px;
  height: 48px;
  place-items: center;
  overflow: hidden;
  border-radius: 50%;
  background: var(--sand);
  color: var(--terracotta);
}
.testimonial-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
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
