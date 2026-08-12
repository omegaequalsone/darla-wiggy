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

All photography lives in `images/` and is served from this repo — nothing is hot-linked
to the old Wix site. Files are named for where they appear (`concert-01.jpg`,
`home-cabaret.jpg`, `hero-portrait.jpg`) rather than for their subject, because most
of the gallery captions in the markup are still `Caption needed` placeholders. Once
the productions are identified, both the captions and the filenames are worth
revisiting.

The one remaining external image is the YouTube poster frame on `cabaret.html`, which
is served from `i.ytimg.com` and belongs to the embedded video.

## Known issues

- **Gallery captions are placeholders.** `concert.html` has 6 and `cabaret.html` has 4
  reading `Caption needed · production, venue, year`. These are visible on the live page.
- **Three images render soft.** The homepage cards are 431x586 boxes, but
  `home-concert.jpg` is only 630x356 — short and wide — so `object-fit: cover` upscales
  it about 1.65x before any Retina scaling. `home-cabaret.jpg` and `home-archive.jpg`
  are close behind, and `concert-05.jpg` is 436x300. Fixing these means going back to
  the original photography; they cannot be recovered by re-encoding.
- **Font licensing is unverified.** Didot HTF and Acid Grotesk are commercial
  typefaces, and this is a public repository.
