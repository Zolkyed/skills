---
name: dark-showcase
description: Applies a quiet, black, premium visual style to any UI without changing its layout: pure black background, near-black surfaces, faded hairline dividers instead of borders, one soft accent glow instead of shadows, a rounded body font with a heavy display face, white headlines over muted gray text, and slow, subtle motion. Use when the user wants a page, app, dashboard or component to look clean, dark and polished, says "style like hayase.watch", "dark showcase style", "make it look premium/clean and dark", or asks to restyle something while keeping its structure. Works with Tailwind (v3 or v4), Svelte, React and plain HTML/CSS.
---

# Dark showcase style

This skill is about **how things look**, not where they go. Keep the existing layout, content, section order and component structure. Change colour, type, lines, depth, surfaces and motion until every element speaks the same quiet visual language.

The style looks expensive because almost everything is silent. Black background, white and gray text, one faint glow. The richness goes into the content itself (media, screenshots, data), never into the chrome.

Reference: the style is modelled on [hayase.watch](https://hayase.watch/) ([hayase-app/website](https://github.com/hayase-app/website)). That code is under the Business Source License, so write the code yourself from these rules: take the look, not the source.

## The style rules

Apply them in this order. Each removes noise before the next adds anything.

### 1. Colour: black, three grays, one accent

| Role | Value | Use |
|---|---|---|
| Page | `#000` | page and every section background |
| Surface | `neutral-950` (`#0a0a0a`) | cards, buttons, inputs, list rows, menus; hover `neutral-900` |
| Line | `#38393c` (centre of a fading gradient) | dividers |
| Hairline | zinc ~16% (`hsl(240 4% 16%)`) | the few solid borders that must stay (inputs, tables) |
| Text | `#fafafa` | headings, labels, button text, values |
| Muted | zinc ~65% (`hsl(240 5% 65%)`) | body copy, captions, meta, placeholders |
| Accent | `#fa68b6` | text selection, the one signature icon |
| Glow | `#ff00b6` at 15% alpha | corner glows only (a more saturated sibling of the accent) |
| Focus ring | zinc ~84% (`hsl(240 5% 84%)`) | 1px ring on buttons and inputs |

- Exactly one accent hue, and it almost never appears at full strength. The one exception is a **signature icon**: a single small accent-coloured icon (a heart on a Donate link, a dot on "Available") with a soft accent drop-shadow and a gentle heartbeat. One per page, in the navbar or footer, never more.
- Primary buttons are white with black text, not accent-coloured.
- No gradient text, no coloured card backgrounds, no second accent. Status colours (red/green) only where they carry meaning, desaturated.
- `color-scheme: dark`, hidden scrollbars, so no browser chrome breaks the black.

### 2. Type: two families, contrast by size and gray

- **Body:** a rounded variable sans (Nunito Variable is the reference), `text-sm` to `text-lg`.
- **Display:** one heavy geometric face (Molot, Russo One or similar) for the wordmark and at most the single largest heading.
- Headings `font-bold`, white, tight leading. Supporting text muted, max ~60ch.
- Hierarchy is size plus white-versus-gray. Never colour, never underline-for-emphasis, never ALL CAPS tracked labels.
- **Outline text** for a giant decorative word: black fill with a 1px `#3a3a3a` text stroke (not text-shadow, which fills the letters) (`ghost` utility). Scale without weight.
- No emoji in UI text.
- **Meta lines** (type · year · status) are spans separated by a tiny gray bullet (`•`, ~0.4rem, `#737373`, a little padding), not commas or pipes.

### 3. Lines: fade, don't box

- Dividers are a **faded hairline**: 1px, transparent → `#38393c` → transparent (`border-gradient`). Use it wherever a solid `border-t`/`border-b` would be.
- Cards and surfaces separate from the page by the `#000` → `neutral-950` step, not by a border.
- Keep solid borders only where function needs them (text inputs, table cells), and then use the hairline gray.
- Radii stay small and consistent: `rounded-md` for controls, `rounded-lg` for cards and media, `rounded-full` only for avatars and pills.

### 4. Depth: glow and blur, never shadow

- No `box-shadow` anywhere. No glassmorphism panels, no gradient blobs.
- **Glow:** a large (~800px) radial gradient of the accent at ~15% alpha fading to transparent. Place it at a **corner of the first screen**, pushed mostly off-screen (e.g. top-right, `translate(70%, -60%)`), so light leaks in from the edge; a second one may sit at the opposite corner of a later section. It should never read as a blob in the middle.
- **Media self-glow:** behind a hero image or video, place a blurred copy (`blur-3xl saturate-200 opacity-60`, slightly larger) so the media lights its surroundings.
- **Edge fades:** black gradients over the ends of anything that bleeds or scrolls (carousels, marquees, long images), so it dissolves into the page instead of being cut.
- Optional, once per page: a slight skew (`matrix(1,0,-.05,1,0,0)`) on a group of screenshots.

### 5. Surfaces and controls

- Card: `bg-neutral-950 rounded-lg`, hover `bg-neutral-900`, `transition`. No border, no shadow.
- Primary button: `bg-white text-black rounded-md font-semibold`. Secondary: `bg-neutral-950 text-white`, hover `neutral-900`. Ghost: text only, muted → white on hover.
- Inputs: `bg-neutral-950`, hairline border, white text, muted placeholder, focus ring in light gray (accent tint optional).
- Icons: lucide, 16–20px, stroke 2, same colour as adjacent text. Brand icons from simple-icons, monochrome white.
- Media: real product imagery or video; muted autoplay loop where motion helps. YouTube embeds can be made ~200px taller than their box and centred to crop the player chrome (see `recipes.md`).
- Logo/favicon: flat, single-colour geometric mark on a square grid, thick bars, sharp diagonals; favicon is the mark in white on a black rounded square.

### 6. Motion: slow and quiet

- Elements fade up once on entering the viewport (opacity 0 → 1, 1.5rem → 0, ~0.7s ease).
- Cards and items that appear dynamically (lists, popovers, previews) **load in** with a short 0.3s ease from `translateY(1.2rem) scale(0.95)` to rest.
- **Press feedback:** every interactive element shrinks to `scale(0.98)` for 0.1s while pressed (`:active`). Exclude sliders and elements marked `no-scale`.
- Loading placeholders are skeleton bars (`bg-white/5 rounded animate-pulse`), the only pulse allowed.
- Continuous motion only for video and marquees, and marquees are slow (100–200s per loop).
- Optional first-load loader: one word revealed by a background-clip wipe.
- Apart from skeletons and the signature icon's heartbeat, nothing pulses, bounces, spins or blinks. Respect `prefers-reduced-motion`.

### 7. Hover: brighten, never recolour

Hover feedback is small and always moves toward white or toward the cursor. It never introduces a new colour.

| Element | Hover | Classes |
|---|---|---|
| Nav, footer and icon links | muted gray → white | `text-muted-foreground hover:text-foreground transition-colors` |
| Cards, list rows, secondary buttons | surface steps up one shade | `bg-neutral-950 hover:bg-neutral-900 transition` |
| Small chips, avatars, logos in a wall | grow slightly | `hover:scale-110 transition-transform` |
| Media thumbnails (episodes, project tiles) | grow to 105% and a black overlay fades to 50% with a white play/open icon | `hover:scale-105 duration-200 ease-out`, overlay `bg-black/0 group-hover:bg-black/50` |
| Text links on content pages | lighter blue | `text-blue-500 hover:text-blue-400` |
| Media preview (video, screenshot) | play button follows the cursor | see "Cursor-follow play button" in `recipes.md` |

- **Cursor-follow play button:** a small round `backdrop-blur` button sits centred on the media with a faint white outer ring. When the pointer enters the media, the button moves to the cursor (position clamped inside the box), the ring disappears, and on direct hover its background fills with white at ~30%. Clicking anywhere opens the full video.
- Use the default transition timing (~150ms). No colour shifts to the accent, no underline animations, no glow on hover, no lift-and-shadow.
- **Hover, focus and press are one state.** Whatever an element does on hover it also does on `:focus-visible` and `:active` (in Tailwind, a custom `select` variant that combines all three keeps this to one class).
- **Focus style:** instead of a coloured ring, a translucent gray fill over the element (`outline: none; border-image: fill 0 linear-gradient(#8883, #8883)`), so focus looks like a soft highlight. A 1px light gray ring is fine on buttons and inputs.
- **Touch devices:** effects that need a pointer (cursor-follow, hover reveals) only apply under `@media (hover: hover) and (pointer: fine)`; on touch, show the resting state and make tap do the action.

### 8. Spacing (consistency only)

The layout is not this skill's business, but the style breaks if spacing is random. Keep whatever structure exists and just make it regular: one container width and gutter, one vertical rhythm between blocks, one gap scale inside components. Generous space reads as premium; tighten only inside dense data.

## Workflow

1. **Read what exists.** Framework, CSS setup, components. Note the layout so you do not change it.
2. **Install the tokens.** Merge `tokens.css` into the global stylesheet (translate the Tailwind v4 `@theme`/`@utility` syntax to `tailwind.config` + `@layer utilities` for v3). Load the fonts.
3. **Strip noise.** Shadows, coloured backgrounds, gradient text, extra accents, emoji, tracked caps labels, solid borders.
4. **Restyle element by element:** colour, type, lines, surfaces and controls, per the rules above.
5. **Add depth:** one glow, media self-glow, edge fades.
6. **Add motion and hover last.**
7. **Verify** in a real browser at desktop and phone width against the checklist, and confirm the layout matches the original. Fix and recheck until it passes.

## Checklist

- [ ] Layout and content unchanged unless the user asked.
- [ ] Backgrounds are `#000`; surfaces are `neutral-950`.
- [ ] One accent hue, only in glow, selection and focus.
- [ ] No `box-shadow`, gradient text, emoji or tracked caps labels.
- [ ] Dividers are faded hairlines; remaining borders are hairline gray.
- [ ] Two font families; display face on the wordmark and at most one heading.
- [ ] Hierarchy readable from size and white/gray alone.
- [ ] Only video, slow marquees, skeletons and the one signature icon move continuously; reduced motion disables animation.
- [ ] Pressing any control gives the 0.98 scale feedback.
- [ ] Every interactive element has a hover state from the hover table, identical on focus and press; none introduces a new colour.
- [ ] Glows sit at screen corners, mostly off-screen.
- [ ] Spacing is regular; no horizontal scroll at 375px.
- [ ] No console errors.

`tokens.css` is the drop-in stylesheet. `recipes.md` has snippets for the effects (hairlines, glow, media self-glow, outline text, edge-faded marquee, reveal, loader, favicon); the markup around them is only an example, keep your own layout.
