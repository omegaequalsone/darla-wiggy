# darla-wiggy

Darla Wigginton website — static HTML site.

## Structure

```
index.html            Home — bio, press quote, Three ways in
concert.html          Concert & Opera
cabaret.html          Cabaret
archive.html          The Archive
home-original.html    Parked: the previous home page, unlinked
fonts/                Didot HTF (regular, bold)
uploads/              Acid Grotesk (regular, bold), logo SVG
images/               All photography
```

Each page is self-contained: styles live in an inline `<style>` block, so there is no
build step and no CSS bundle to keep in sync. Edit the HTML directly.

There is no About page. Its content is the home page — reachable via the logo. The nav
is Concert & Opera / Cabaret / The Archive.

`home-original.html` is a snapshot of the home page as it stood before that swap, kept
so material can be pulled back out of it. It is deliberately untouched, so it still
carries the old nav, the old footer, and links to the deleted `about.html`. Nothing
links to it.

## Running locally

```bash
python3 -m http.server 8000
```

Then open http://127.0.0.1:8000.

**Do not open the `.html` files by double-clicking them.** Over `file://` the browser
blocks local subresources, so every image and every self-hosted font silently fails and
the page looks broken when it is not. If images disappear, check the URL bar first.

## Typography

- **Didot HTF** — display serif, self-hosted from `fonts/`
- **Acid Grotesk** — sans, self-hosted from `uploads/`
- **IBM Plex Mono** — labels and eyebrow text, loaded from Google Fonts

## Conventions worth keeping

**Small text uses `#8c8377`.** On the `#100e0c` ground that clears WCAG AA at 5.16:1.
The greys it replaced (`#6f665a` at 3.42:1, `#4a443c` at 2.00:1) did not. Don't
reintroduce them for anything under 18px.

**Empty `<figcaption>` elements are hidden**, via `figcaption:empty { display: none; }`.
An uncaptioned photograph therefore shows no placeholder text and leaves no gap, and
adding a caption later is just typing between the tags. Note `:empty` only matches when
there is *no* whitespace inside — keep the tags flush.

**The home hero fades at its left and bottom edges** using a CSS `mask-image`, not an
overlay. The source JPEG is untouched. Two mask layers need `mask-composite: intersect`,
so the rule is wrapped in `@supports`; without it the layers would union and cancel the
fade. Ramp lengths are the `--fade-x` / `--fade-y` variables. That hero section carries
no `border-bottom` on purpose — a hairline there redraws the edge the mask dissolves.

**Archive filters** are real `<button>`s carrying `aria-pressed`, so they are keyboard
operable and state cannot drift from styling. Rows carry `data-cats` (space-separated,
multi-category) and `data-year`. Decade chips are generated from the rows, so a decade
with no engagements never appears. Every count on the page is derived from the DOM
rather than hardcoded.

## Images

All photography lives in `images/` and is served from this repo — nothing is hot-linked
to the old Wix site. The one remaining external image is the YouTube poster frame on
`cabaret.html`, served from `i.ytimg.com`, which belongs to the embedded video.

Most of the collection is fine. Measured against the real layout at 2x, 10 of 16 images
render at or below 1.0x and are sharp; the softness is concentrated in a few slots.

## Known issues

- **Gallery captions are empty.** `concert.html` has 6 and `cabaret.html` has 4 with no
  caption. They are hidden rather than showing placeholder text, so nothing is broken on
  the page — but the productions are still unidentified.
- **`home-concert.jpg` is the weakest asset on the site.** It is 630x356 filling a
  513x602 card, which is a 3.38x upscale *and* roughly a 50% width crop, because a
  1.77:1 landscape is being forced into a 0.85:1 portrait slot. Higher resolution alone
  will not fix it; the aspect mismatch is the larger half of the problem.
- **`home-cabaret.jpg` and `home-archive.jpg` are soft on Retina only** (1.77x / 1.76x).
  Both are 1024x680, which is a perfectly good file — the card box is simply oversized.
  Capping the cards at 380px wide takes them to 1.31x with no new photography.
- **`concert.html` overstates the Archive.** Its link reads "All 200+ chorus
  productions", but the Archive holds 18 rows, 4 of them chorus.
- **The site has no contact route.** Removing the footer took
  `hello@darlawigginton.com` with it. There is no email, booking or social link.
