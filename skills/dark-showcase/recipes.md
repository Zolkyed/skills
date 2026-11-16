# Recipes

Plain HTML with Tailwind classes. Translate to the project's framework (Svelte, React, etc.). These are style effects: the surrounding markup is only an example, so apply the classes and effects to the project's existing structure instead of copying the layout.

## Hero video with cropped YouTube chrome and self-glow

```html
<section class="relative w-full max-w-screen-xl mx-auto px-12 pt-32">
  <!-- ambient glow -->
  <div class="glow absolute inset-x-0 -top-40 h-[800px] pointer-events-none"></div>

  <div class="relative aspect-video">
    <!-- blurred copy: the media lights its own surroundings -->
    <div class="absolute -inset-8 overflow-hidden blur-3xl saturate-200 opacity-60 pointer-events-none">
      <iframe class="absolute left-0 top-1/2 w-full h-[calc(100%+200px)] -translate-y-1/2"
        src="https://www.youtube-nocookie.com/embed/VIDEO_ID?autoplay=1&mute=1&loop=1&controls=0&playlist=VIDEO_ID"
        allow="autoplay" tabindex="-1" title=""></iframe>
    </div>
    <!-- sharp copy, ~200px taller than the box so the player chrome is cropped -->
    <div class="relative h-full overflow-hidden rounded-lg pointer-events-none">
      <iframe class="absolute left-0 top-1/2 w-full h-[calc(100%+200px)] -translate-y-1/2"
        src="https://www.youtube-nocookie.com/embed/VIDEO_ID?autoplay=1&mute=1&loop=1&controls=0&playlist=VIDEO_ID"
        allow="autoplay" title="Product preview"></iframe>
    </div>
    <!-- click target that opens the full video in a dialog -->
    <button class="absolute inset-0" aria-label="Play video"></button>
  </div>
</section>
```

With a local file, use `<video autoplay muted loop playsinline>` for both copies instead of iframes; no crop needed.

## Cursor-follow play button

The button rests in the centre. While the pointer is over the media it follows the cursor, loses its white ring, and turns translucent white on direct hover.

```html
<div class="play-area group relative overflow-hidden rounded-lg" style="--x:50%; --y:50%">
  <!-- media here -->
  <button aria-label="Play video"
    class="absolute z-10 size-10 rounded-full grid place-items-center backdrop-blur
           -translate-x-1/2 -translate-y-1/2 left-1/2 top-1/2
           group-hover:left-[var(--x)] group-hover:top-[var(--y)]
           shadow-[0_0_0_1px_#fff6] group-hover:shadow-none hover:bg-white/30
           transition-[background-color,box-shadow] focus-visible:ring-2 focus-visible:ring-neutral-300">
    <svg class="size-4 fill-white" viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg>
  </button>
</div>

<script>
  for (const area of document.querySelectorAll('.play-area')) {
    area.addEventListener('pointermove', (e) => {
      const r = area.getBoundingClientRect()
      const x = Math.min(Math.max(e.clientX - r.left, 0), r.width)
      const y = Math.min(Math.max(e.clientY - r.top, 0), r.height)
      area.style.setProperty('--x', x + 'px')
      area.style.setProperty('--y', y + 'px')
    })
    area.addEventListener('click', () => { /* open the video dialog */ })
  }
</script>
```

Position changes are not transitioned, so the button tracks the cursor exactly; only its background and ring animate.

## Section with faded hairline

```html
<section class="max-w-screen-xl mx-auto px-12 py-24 border-t border-gradient">
  <h2 class="text-4xl md:text-5xl font-bold text-white">One clear claim.</h2>
  <p class="mt-4 max-w-[60ch] text-muted-foreground text-lg">One sentence that backs it up.</p>
</section>
```

Two columns split by a vertical hairline: give the second column `lg:border-l border-gradient` (the gradient is horizontal, so for a vertical line swap `90deg` for `180deg` in a separate utility).

## Outline headline behind a solid one

```html
<div class="relative text-center">
  <div class="ghost font-display text-[18vw] leading-none select-none" aria-hidden="true">NAME</div>
  <h1 class="absolute inset-0 flex items-center justify-center text-6xl font-bold">Real headline</h1>
</div>
```

## Card

```html
<a href="#" class="flex flex-col p-6 rounded-lg bg-neutral-950 hover:bg-neutral-900 transition">
  <svg class="size-6"><!-- lucide icon --></svg>
  <div class="mt-3 text-lg font-semibold">Title</div>
  <div class="text-muted-foreground text-sm">One muted line.</div>
</a>
```

## Marquee wall

Duplicate each row's items so translating by -50% loops seamlessly.

```html
<div class="relative overflow-clip max-w-[1600px] mx-auto">
  <div class="fade-x absolute inset-0 z-10 pointer-events-none"></div>
  <div class="marquee-row"><!-- items ×2 --></div>
  <div class="marquee-row"><!-- items ×2 --></div>
</div>

<style>
  .marquee-row { width: max-content; white-space: nowrap; animation: marquee 200s linear infinite; }
  .marquee-row:nth-child(odd of .marquee-row) { animation-direction: reverse; }
  @keyframes marquee { to { transform: translateX(-50%); } }
</style>
```

Chip: `inline-flex items-center gap-2 m-2 px-4 py-3 rounded bg-neutral-950 text-xs font-bold hover:scale-110 transition-transform` with a `size-6 rounded-full` avatar.

## Scroll reveal

```js
const io = new IntersectionObserver((entries) => {
  for (const e of entries) if (e.isIntersecting) { e.target.classList.add('shown'); io.unobserve(e.target) }
}, { threshold: 0.15 })
document.querySelectorAll('.reveal').forEach((el) => io.observe(el))
```

In Svelte, wrap this in an action (`use:reveal`); in React, a small `useReveal` ref hook.

## Loader word wipe

```html
<div id="loader" class="fixed inset-0 z-50 grid place-items-center bg-black">
  <span class="loader-text font-display text-3xl">Loading...</span>
</div>

<style>
  .loader-text {
    color: transparent;
    background: linear-gradient(90deg, #fff 50%, #333 50%) right / 200% 100% no-repeat;
    -webkit-background-clip: text; background-clip: text;
    animation: wipe 1.2s ease forwards;
  }
  @keyframes wipe { to { background-position: left; } }
</style>
```

Remove the loader on `load` (or after fonts are ready) with a short opacity fade.

## Favicon from the logo mark

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 64 64">
  <rect width="64" height="64" rx="14" fill="#000"/>
  <path fill="#fff" transform="translate(13 13) scale(0.57)" d="<mark path on a ~66 unit grid>"/>
</svg>
```
