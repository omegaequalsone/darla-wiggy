# darla-wiggy

Darla Wigginton website — static HTML site.

## Structure

```
index.html      Home
concert.html    Concert & Opera
cabaret.html    Cabaret
archive.html    The Archive
about.html      About
fonts/          Didot HTF (regular, bold)
uploads/        Acid Grotesk (regular, bold), logo SVG
```

Each page is self-contained: styles live in an inline `<style>` block, so there is no
build step and no CSS bundle to keep in sync. Edit the HTML directly.

## Running locally

```bash
python3 -m http.server 8000
```

Then open http://127.0.0.1:8000.

Opening the `.html` files directly via `file://` will not work — the `@font-face` rules
need to be served over HTTP.

## Typography

- **Didot HTF** — display serif, self-hosted from `fonts/`
- **Acid Grotesk** — sans, self-hosted from `uploads/`
- **IBM Plex Mono** — labels and eyebrow text, loaded from Google Fonts

## Images

Photography is currently hot-linked from `static.wixstatic.com` (the previous Wix site).
These are not stored in this repo, so the images depend on that Wix account staying
active. See the open issues below.

## Known issues

- **Images are hot-linked to Wix.** If the Wix site lapses, every photo on the site
  breaks. They should be downloaded, optimized, and committed here.
- **Unoptimized source images.** At least one hot-linked asset is a 5 MB PNG being
  scaled down in the browser.
- **Font licensing is unverified.** Didot HTF and Acid Grotesk are commercial
  typefaces, and this is a public repository. Confirm the licenses permit web
  embedding and redistribution before treating this as settled.
