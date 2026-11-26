# Fuel Your Fitness

Mobile-first catalogue website for **Fuel Your Fitness**, a genuine supplements store in India. Visitors browse products by brand or category, search the catalogue, and place orders through Instagram DM.

**Live site:** https://fuelyourfitness.in
**Instagram:** [@fuelyourfitness.in](https://www.instagram.com/fuelyourfitness.in/)

---

## Features

- Shop by **brand** (12 brands) and by **category** (Whey, Mass Gainer, Creatine, Pre-Workout, BCAA/EAA, Multivitamin, Fish Oil)
- **Search** by brand, product or category. Works with the Search button, the Enter key and the mobile keyboard's search key. Every word you type must match, so `muscle blaze whey` finds the right products
- Category chips to filter the product grid
- Real product photos with an automatic fallback to a generated bottle illustration if a photo is missing
- **Order on Instagram** button on every product, which opens an Instagram DM and copies a ready order message
- Responsive layout with a sticky header, bottom navigation bar and a scrolling highlights strip
- No framework, no build step, no dependencies

## Tech stack

| Part | Choice |
|------|--------|
| Frontend | Plain HTML, CSS and vanilla JavaScript (single `index.html`) |
| Fonts | Google Fonts (Barlow, Barlow Condensed) |
| Hosting | [Render](https://render.com) static site |
| Domain | `fuelyourfitness.in` (GoDaddy) |

## Project structure

```
.
├── index.html        # The whole website (HTML + CSS + JS)
├── logo.jpg          # Store logo, favicon and share image
├── render.yaml       # Render static site configuration
├── images/           # Product photos (see naming below)
└── logos/            # Optional brand logos
```

## Run locally

No installation needed. Either open `index.html` in a browser, or serve the folder:

```bash
# Python
python3 -m http.server 8000

# or Node
npx serve .
```

Then open http://localhost:8000.

## Adding or editing products

All products live in the `B` object near the top of the `<script>` in `index.html`:

```js
"BrandName": ["AB", "#f5b800", "#111", [
  [0, "Product Name"],   // [category index, product name]
  [2, "Another Product"]
]]
```

- `AB` is the short label, then the brand colour, then the label text colour
- Category indexes: `0` Whey Protein, `1` Mass Gainer, `2` Creatine, `3` Pre-Workout, `4` BCAA / EAA, `5` Multivitamin, `6` Fish Oil & More

To add a new brand, add a new entry to `B`. It appears in the brand row and the product grid automatically.

## Product photos

Put photos in the `images/` folder, named `<brand>-<product>` in lowercase with hyphens:

| Product | File name |
|---------|-----------|
| MuscleBlaze Whey Gold Isolate | `images/muscleblaze-whey-gold-isolate.jpg` |
| Optimum Nutrition Gold Standard 100% Whey | `images/optimum-nutrition-gold-standard-100-whey.jpg` |

- Supported formats: `webp`, `jpg`, `png`, `jpeg` (tried in this order)
- Recommended: square, around 600×600 px, product centred on a plain background
- A product without a photo shows a generated bottle illustration instead, so nothing breaks

**Brand logos** (optional) go in `logos/<brand>.png`, for example `logos/muscleblaze.png`. Supported formats: `png`, `webp`, `svg`, `jpg`.

## Deployment (Render)

The site is a static site, so there is nothing to build.

`render.yaml`:

```yaml
services:
  - type: web
    name: fuel-your-fitness
    runtime: static
    staticPublishPath: .
```

1. Push the repo to GitHub.
2. In Render, create a **Static Site** from the repo (or use the Blueprint with `render.yaml`).
3. Every push to the main branch redeploys automatically.

### Custom domain (GoDaddy)

1. In Render, open the service, go to **Settings → Custom Domains**, and add `fuelyourfitness.in` and `www.fuelyourfitness.in`.
2. In GoDaddy DNS, add the records Render shows you (usually an `A` record for the root domain and a `CNAME` for `www`).
3. Wait for DNS to propagate. Render then issues the HTTPS certificate automatically.

## Contact

Orders and price enquiries: message [@fuelyourfitness.in](https://ig.me/m/fuelyourfitness.in) on Instagram.

## Disclaimer

Brand names and logos belong to their respective owners and are used only to identify the products sold. Consult a doctor before using supplements if you have a medical condition.
