# sunatyam.com

The single-page marketing site for **Sunatyam Studios**, served by GitHub Pages at
<https://sunatyam.com>.

There is no build step. `index.html` is the whole site — HTML, CSS and JS in one
file. Open it in a browser to see exactly what production looks like. The only
external request the page makes is to Google Fonts.

```
index.html         the entire page: markup, inline <style>, inline <script>
CNAME              custom domain — must stay in sync with Settings → Pages
.nojekyll          tells Pages to serve files as-is, no Jekyll processing
robots.txt         allow-all + sitemap pointer
sitemap.xml        one URL
favicon.svg        the tala mark (sam stroke + beats)
site.webmanifest   name, colours, icon
og-image.png       PLACEHOLDER — see the checklist below
```

---

## Editing the copy

All text lives in `index.html`. The sections are separated by comment banners
(`<!-- ============ 3. KOSHA ============ -->`) in page order:

| # | `id` | What it is |
|---|---|---|
| 1 | `top` | Hero, plus the "Sunatyam is early" stage note |
| 2 | `intent` | What the work is for — rasa, sadharanikarana |
| 3 | `kosha` | The library: what it holds, how it opens |
| 4 | `route` | The five-step route for creators |
| 5 | `rights` | Rights, credit, payment standards |
| 6 | `terms` | Visibility levels — the tabbed block |
| 7 | `who` | Who this is for |
| 8 | `rules` | House rules |
| 9 | `status` | **Where we actually are** |
| 10 | `contact` | Three mailto routes |

Two conventions worth keeping:

- **Tense.** Anything operational is written in future/intentional tense ("what
  we're building", "the standard we're writing toward"). Present tense is reserved
  for values and principles. The company is in planning and the page should keep
  saying so until it isn't.
- **No invented specifics.** No prices, dates, view counts, testimonials, awards,
  team names, parent company, production partners, or named productions.

### Keep the status section current

Section 9 (`id="status"`) is the one part of this page that goes stale on its own,
and a stale status is worse than no status — it turns the most honest section into
the least. There's a comment in the file saying so. Five rows, each with a chip:

```html
<span class="st-chip"><span class="chip">In progress</span></span>   <!-- gold  -->
<span class="st-chip"><span class="chip off">Not open</span></span>  <!-- grey  -->
```

Add `off` to the chip for anything not yet open.

### Design tokens

Colours, fonts and spacing are CSS custom properties on `:root` at the top of the
`<style>` block — change them there, not inline.

| Token | Value | Use |
|---|---|---|
| `--nishi` | `#0B1220` | pre-dawn indigo, page ground |
| `--pradip` | `#E3A94B` | lamp brass, accent — sparingly |
| `--shola` | `#F4EFE6` | warm off-white, headings |
| `--fg` | `#CBD3E0` | body copy |
| `--dhusar` | `#93A2B8` | secondary text, eyebrows |

Two devices carry the identity and shouldn't be removed casually:

- **`.rule`** — the hairline above every section is a *tala cycle*: a tall gold
  stroke at the left marking *sam*, then faint ticks for the beats after it. Pure
  CSS, no images. A tala is common to every Indian tradition, which is the point —
  the studio is pan-Indian, not regional.
- **`--dawn`** — a fixed gradient layer behind the page whose opacity tracks scroll
  progress, so the room lightens as you read down it. Capped at `0.88` so body text
  never drops below WCAG AA. If you change the gradient, re-check contrast at the
  bottom of the page.

Both respect `prefers-reduced-motion`.

---

## DNS

The apex domain points straight at GitHub Pages. Records below are the values
GitHub currently documents in *"Managing a custom domain for your GitHub Pages
site"* — re-check that page rather than copying these from memory if you ever
rebuild the zone.

**Four `A` records** — host `@` (apex, `sunatyam.com`):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**Four `AAAA` records** — host `@`, for IPv6:

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

**One `CNAME` record** — host `www` → `sunatyam.github.io.`

Notes:

- The `CNAME` file in this repo root must contain exactly `sunatyam.com`. GitHub
  writes this file itself when you set the custom domain under Settings → Pages;
  the committed file and the setting must agree or Pages will fight you.
- Propagation can take up to 24 hours. `dig sunatyam.com +short` should return the
  four A records once it has landed.
- **Enforce HTTPS** only becomes available in Settings → Pages *after* GitHub has
  issued the certificate, which it can't do until DNS resolves. Check back and turn
  it on — it isn't automatic.

## Deploying

Pushing to `main` deploys. Settings → Pages → Source: *Deploy from a branch* →
branch `main`, folder `/ (root)`.

---

## Pre-launch checklist

- [ ] Replace `og-image.png` with a real 1200×630 image (the current one is a
      generated placeholder — flat colour and rules, no type)
- [ ] Write `/terms` and `/privacy`, including the registered entity and a named
      contact. No company is named anywhere on the page, so these two carry the
      site's legitimacy
- [ ] Confirm `hello@sunatyam.com` and `studio@sunatyam.com` exist and are monitored
- [ ] Set the five "Where we actually are" statuses to what is genuinely true
- [ ] Decide whether to add a city under "India" in the footer — a location adds
      credibility
- [ ] Have the Kosha licensing language reviewed by a media/IP advocate before any
      licence is offered
