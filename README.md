<div align="center">

# Filaxy PDF Converter — Landing

**The marketing site for [Filaxy PDF Converter](https://github.com/othmarodev/filaxy-pdf-converter)** — a free,
open-source macOS app that converts any PDF into a faithful, editable Word document, then verifies its own
work line by line.

### → [pdfconverter.filaxy.net](https://pdfconverter.filaxy.net) ←

Bilingual (EN/ES) · Light & dark · Fully self-contained · Zero build step · Zero dependencies

</div>

---

## What this is

A single, hand-written `index.html` (~860 lines) with all CSS and JavaScript embedded — no framework, no
bundler, no npm install, nothing to compile. It drops straight onto Cloudflare Pages as static files. The
whole thing is built to feel like a premium product page (Apple / Stripe / Linear tier) while staying a
few kilobytes of plain web platform.

## Highlights & effects

Every effect is pure CSS/Canvas/vanilla JS and degrades gracefully under `prefers-reduced-motion`.

| Effect | How it's done |
| --- | --- |
| 🌧️ **PDF rain background** | A full-page `<canvas id="bg">` renders falling PDF-page silhouettes (folded corner + red badge) that drift, rotate, and react to the cursor — they nudge aside and glow when the mouse gets close. |
| 🔦 **Cursor spotlight** | A fixed radial glow tracks the pointer via CSS custom properties (`--mx` / `--my`), blended with `mix-blend-mode` (screen in dark, multiply in light). |
| 🎴 **3D card tilt** | Cards tilt toward the cursor on `pointermove` and carry an internal moving sheen (`--cx` / `--cy`). |
| ✨ **Neon border beams** | A rotating conic-gradient masked to a 1.5px ring (via `@property --beam` + `mask-composite: exclude`) sends a light beam traveling around every card border. Neighbours are phase-offset so they never march in lockstep. |
| ✅ **Live self-verification** | When the "It checks its own work" section scrolls into view, a scan beam sweeps down the card and each row ticks green **in sequence** — the check circle pops grey→green, the checkmark draws itself with `stroke-dashoffset`, and the status label lights up. It mirrors what the actual app does. |
| 🎞️ **Animated trust strip** | A red light sweep glides across the trust badges; items stagger in and lift on hover. |
| 🏷️ **Infinite marquee** | A paused-on-hover marquee of the document types the app is built for (salary certificates, invoices, contracts, bank statements…). |
| 🖼️ **Lightbox gallery** | Real app screenshots open full-screen on click; close with ×, `Esc`, or click-outside. |
| 🎈 **Floating hero badge** | A "100% verified" badge pulses over the hero window mockup. |
| 🌗 **Anti-flash theming** | An inline `<head>` script sets the theme before first paint (defaults to **dark**), so there's no white flash on load. |
| 🌍 **Live EN/ES switch** | Language toggles instantly with no reload — every string ships in both languages and is shown/hidden via `data-lang`. |
| 🎬 **Scroll reveals** | Sections fade/slide in with an `IntersectionObserver`, with staggered delays for grids. |

## Tech stack

- **HTML5** — semantic, single file, all content inline.
- **CSS** — modern features only: custom properties, `color-mix()`, `@property` registered custom properties,
  `conic-gradient`, CSS masking, `mix-blend-mode`, container-free responsive layout with `clamp()` and grid.
- **Vanilla JavaScript** — no libraries. Canvas animation loop, `IntersectionObserver` reveals, pointer-driven
  tilt/spotlight, theme + language state in `localStorage`, lightbox.
- **System font stack** — `-apple-system` / Segoe UI / Inter fallback. No web-font requests.
- **Icons** — inline SVG, no icon library.
- **Build** — none. **Dependencies** — none.

## Design system

Colors are derived from the app icon, not the usual Filaxy violet→sky.

- **Brand red** `#D8131E` (light) / `#FF3B45` (dark), with a warmer coral `#F0453C` / `#FF6A5A` accent used
  for the neon beams.
- Near-black `#0B0A0B` dark canvas; clean white light theme.
- Theme tokens live in `:root` + `html[data-theme="…"]`; the palette drives every gradient, glow, and beam.

## Accessibility & performance

- Full **`prefers-reduced-motion`** support — the canvas, spotlight, beams, marquee, and reveals all stand down.
- Decorative layers are `aria-hidden`; the language switch keeps `<html lang>` in sync.
- Readable footer and nav contrast in **both** themes.
- No render-blocking fonts or scripts; assets are ~670 KB total (mostly real screenshots).

## Page structure

`nav → hero (window mockup + pulsing badge) → trust strip → document-type marquee → "It checks its own work"
→ features bento → how it works → screenshot gallery → download (Homebrew + Apple Silicon/Intel) → support
(PayPal + USDT TRC20) → closing CTA → footer`

## Project layout

```
.
├── index.html            # the entire site — CSS + JS embedded
├── assets/
│   ├── icon.png          # app icon
│   ├── icon-180.png      # apple-touch-icon / favicon
│   ├── usdt-qr.png       # TRC20 donation QR
│   └── screens/          # real app screenshots (verify dark/light/es, how-it-works)
├── LICENSE               # MIT
└── README.md
```

## Local development

No tooling required — just serve the folder over HTTP:

```bash
python3 -m http.server 8770
# → http://localhost:8770
```

> Assets use absolute paths (`/assets/…`), so open it over **HTTP**, not `file://`, or images will 404.

## Deployment

Deployed as static files to **Cloudflare Pages** (direct upload):

```bash
wrangler pages deploy . --project-name filaxy-pdf-converter-site --branch main
```

The custom domain `pdfconverter.filaxy.net` is attached to the Pages project and served over Cloudflare's edge.

## Links

- 🌐 **Live site:** https://pdfconverter.filaxy.net
- 📦 **The app:** https://github.com/othmarodev/filaxy-pdf-converter
- 🧰 **Filaxy Labs:** https://filaxylabs.co

## License

[MIT](LICENSE) © Othmaro Fallas Rojas
