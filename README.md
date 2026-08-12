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
to the old Wix site. Filenames carry the first eight characters of the original Wix
asset hash, so they are stable but not descriptive; they can be renamed to something
readable as long as the references in the HTML are updated to match.

The one remaining external image is the YouTube poster frame on `cabaret.html`, which
is served from `i.ytimg.com` and belongs to the embedded video.

## Known issues

- **Some source images are low resolution.** Several are only 400–700 px wide, which
  is soft on high-density displays. They were that size on Wix; improving them means
  going back to the original photography.
- **Font licensing is unverified.** Didot HTF and Acid Grotesk are commercial
  typefaces, and this is a public repository.
