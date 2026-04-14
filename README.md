# beaconstack.io

Marketing and documentation site for the [Beacon media stack](https://github.com/beacon-stack).

Built with Astro + Tailwind CSS v4. Deployed to GitHub Pages at [beaconstack.io](https://beaconstack.io).

## Local development

```sh
npm install
npm run dev
```

Opens at `http://localhost:4321`.

## Build

```sh
npm run build    # output goes to dist/
npm run preview  # serve the built output locally
```

## Deployment

Pushes to `main` trigger the GitHub Actions workflow at `.github/workflows/deploy.yml`,
which builds the site and deploys to GitHub Pages using `actions/deploy-pages`.

Before the first deploy:
1. Create the GitHub repo under the `beacon-stack` org: `beacon-stack/beaconstack.io`
2. In repo Settings > Pages: set Source to "GitHub Actions"
3. Add a CNAME record for `beaconstack.io` pointing to `beacon-stack.github.io`
   (the `public/CNAME` file is already in place)

## Adding screenshots

Screenshots belong in `public/screenshots/`. Drop them there and update the
placeholder `<div class="screenshot-placeholder">` blocks in the relevant page:

| Placeholder | File to drop |
|---|---|
| Pulse dashboard | `public/screenshots/pulse-dashboard.png` |
| Pilot series library | `public/screenshots/pilot-library.png` |
| Pilot search modal | `public/screenshots/pilot-search-modal.png` |
| Pilot calendar | `public/screenshots/pilot-calendar.png` |
| Pilot wanted page | `public/screenshots/pilot-wanted.png` |
| Prism movie grid | `public/screenshots/prism-library.png` |
| Prism search scoring | `public/screenshots/prism-search.png` |
| Prism release decision | `public/screenshots/prism-release-decision.png` |
| Haul main list | `public/screenshots/haul-torrents.png` |
| Haul dashboard | `public/screenshots/haul-dashboard.png` |
| Haul torrent detail | `public/screenshots/haul-detail.png` |

Replace the placeholder `<div>` with:

```astro
<img
  src="/screenshots/filename.png"
  alt="[descriptive alt text]"
  loading="lazy"
  class="screenshot"
/>
```

And add to the page's `<style>`:

```css
.screenshot {
  width: 100%;
  border-radius: 6px;
  border: 1px solid var(--color-border-2);
}
```

## Design decisions (v2)

**Type.** Inter (UI, all weights) + JetBrains Mono (code only). Inter at 700–900
with -0.04em letter-spacing reads modern and structural. No display serifs anywhere.
Mono is strictly scoped to code blocks and inline technical references — body copy
is Inter 400/500 at comfortable size and line-height.

**Palette.** Dark-first. Background is `#0d0f14` (near-black with a cool blue
undertone). Primary accent is `#00b4d8` (cyan-teal) — reads "signal" and stays
well clear of the indigo/violet AI-site cluster. Secondary emphasis color is
`#e8a838` (amber-gold), used sparingly for semantic markers, overlines, and HTTP
method badges. All color tokens are defined as CSS custom properties in `@theme`
with semantic names so the whole palette can be retuned in one file.

**Layout.** Dark-panel hero with a two-column grid (title/subtitle/CTAs left,
hub animation right). App cards on the homepage are a 2x2 bordered grid — not
identical icon cards. App pages use a two-column deep-dive layout (heading anchored
left in a fixed column, content and code blocks flowing right). Code blocks have
a dark window treatment with a bar, monospace text, and syntax coloring that
integrates into the page rather than floating as afterthoughts.

**Animations.** SVG + CSS `animateMotion` for the hub diagram; CSS keyframe
`translateY` + `opacity` for the registration exchange. No GIF, no canvas,
no library. Both respect `prefers-reduced-motion` via the global CSS rule.

**No frameworks.** Astro components only, with scoped `<style>` blocks.
The two animations are pure SVG/CSS.

## Project structure

```
src/
  layouts/
    Base.astro        Persistent header, footer, font imports
  pages/
    index.astro       Ecosystem overview + animations
    pulse.astro       Pulse deep-dive
    pilot.astro       Pilot deep-dive
    prism.astro       Prism deep-dive
    haul.astro        Haul deep-dive
  styles/
    global.css        Design tokens (@theme), resets, base typography
public/
  CNAME               beaconstack.io
  favicon.svg
.github/
  workflows/
    deploy.yml        Build + deploy on push to main
```
