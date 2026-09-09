# road-trip

A single-page trip planner, served by GitHub Pages at
<https://zangelchen.github.io/road-trip/>.

## Files

| Path | What it is |
|---|---|
| `index.html` | The whole site: markup and a small vanilla-JS controller. No build step. |
| `styles.css` | All styling. Design tokens live at the top, in `:root` and the two dark-mode blocks. |
| `img/` | Web assets the page actually loads — resized to ~900–1100px and compressed. |
| `images/` | The original downloads, kept as the source for re-editing. Never served. |

## How it works

Three top-level tabs — Itinerary, Rental Car, Other Options. Each tab holds a
chooser of destination cards; picking one hides the chooser and reveals that
destination's section. Sections can carry a segmented control for variants
(itinerary length, transport, or Lodging / Things to do).

The controller is about 150 lines at the bottom of `index.html`:

- `showView(key)` switches the top-level tab.
- `openRoute(view, key, version)` opens a destination inside its own view.
- `setVersion(routeEl, version)` switches the segmented control. Blocks marked
  `data-only="v1 v2"` are shown only for the variants they name.
- The hotel table sorts on any `<th class="sortable">` and filters on the
  `.fbtn` chips.

## Adding things

- **A destination**: copy a whole `<section class="route" id="route-…">` block
  and its `.optcard` in the chooser. No JavaScript changes needed — routes are
  discovered from the DOM.
- **A hotel**: add a `<tr>` to the table. `data-sort` on the date and price
  cells is what the sorter reads, so keep it in ISO / plain-number form.
- **A photo**: put the web-sized file in `img/`, the original in `images/`, and
  give the `<img>` explicit `width`, `height` and `loading="lazy"`.

## Access

The page has a password screen. It is a convenience, not security: this is a
static site, so the password and everything behind it are readable in the
source. Nothing sensitive belongs on this page.
