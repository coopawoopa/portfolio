<script>
  import { onMount } from 'svelte';

  let container;
  let cards;

  const CONFIG = {
    proximity: 20,
    spread: 300,
    blur: 120,
    gap: 32,
    opacity: 0,
    delay: 1 // delay in seconds
  };

  const updateGlow = (event) => {
    for (const card of cards) {
      const cardBounds = card.getBoundingClientRect();
      const isWithinProximity = (
        event.clientX > cardBounds.left - CONFIG.proximity &&
        event.clientX < cardBounds.left + cardBounds.width + CONFIG.proximity &&
        event.clientY > cardBounds.top - CONFIG.proximity &&
        event.clientY < cardBounds.top + cardBounds.height + CONFIG.proximity
      );

      card.style.setProperty('--active', isWithinProximity ? 1 : CONFIG.opacity);

      const cardCenter = [
        cardBounds.left + cardBounds.width * 0.5,
        cardBounds.top + cardBounds.height * 0.5,
      ];

      let angle = Math.atan2(event.clientY - cardCenter[1], event.clientX - cardCenter[0]) * 180 / Math.PI;
      angle = angle < 0 ? angle + 360 : angle;
      card.style.setProperty('--start', angle + 90);
      card.style.setProperty('--spread', `${CONFIG.spread}px`);
    }
  };

  onMount(() => {
    container = document.querySelector('.container');
    cards = document.querySelectorAll('article');
    document.body.addEventListener('pointermove', updateGlow);
  });
</script>

<div class="container">
<article>

  <slot></slot>
</article>
</div>

<style>
html, body {
  margin: 0px 0; 
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  position: relative;
  touch-action: none;
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

article {
  --active: 0.15;
  --start: 0;
  --spread: 300px;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0rem;
  float: none;
}

.glows {
  pointer-events: none;
  position: absolute;
  inset: 0;
  filter: blur(var(--spread));
}

.glows::after,
.glows::before {
  content: "";
  background: conic-gradient(from 180deg at 50% 70%, hsla(0, 0%, 98%, 1) 0deg, #ff0266 72deg, #ff0266 144deg, #ff0266 216deg, #ffffff 288deg, hsla(0, 0%, 98%, 1) 1turn);
  background-attachment: fixed;
  position: absolute;
  border: 10px solid transparent;
  border-radius: 12px;
  mask: linear-gradient(#0000, #0000), conic-gradient(from calc((var(--start) - 40) * 1deg), #000 0deg, #fff, #0000 calc(80 * 1deg));
  mask-composite: intersect;
  mask-clip: padding-box, border-box;
  opacity: var(--active);
  transition: opacity 3s;
}

article::before {
  position: absolute;
  inset: 0;
  border: 2px solid transparent;
  content: "";
  border-radius: 12px;
  pointer-events: none;
  background: hsl(280, 10%, 50% / 1);
  background-attachment: fixed;
  mask: linear-gradient(#0000, #0000), conic-gradient(from calc(((var(--start) + 20) - 100) * 1deg), hsl(0, 0%, 100% / 0.15) 0deg, white, hsl(0, 0%, 100% / 0.15) calc(100deg));
  mask-clip: padding-box, border-box;
  mask-composite: intersect;
  opacity: var(--active);
  transition: opacity 1s;
}

article::after {
  content: "";
  pointer-events: none;
  position: absolute;

  background-attachment: fixed;
  border-radius: 12px;
  opacity: var(--active, 0);
  transition: opacity 0.1s;
  inset: 0;
  border: 2px solid transparent;
  mask: linear-gradient(#0000, #0000), conic-gradient(from calc(((var(--start) + 20) - 40) * 1deg), #0000 0deg, #fff, #0000 calc(100deg));
  filter: brightness(0.2);
  mask-clip: padding-box, border-box;
  mask-composite: intersect;
  overflow: hidden;
  z-index: 0;
}
</style>
