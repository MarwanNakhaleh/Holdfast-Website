# Holdfast-Website

Static site for [Holdfast](https://github.com/MarwanNakhaleh/HoldfastBrickAPI):
what it is, how to build one yourself, and (eventually) the pre-built kit.

No build step — plain HTML/CSS/JS. Open `index.html` in a browser, or serve
the folder with anything (`python3 -m http.server`).

| Path | What it is |
|---|---|
| `index.html` | The landing page (current pick from the design directions) |
| `guide.html` | Full DIY setup guide: flash the Pi, plug into the router, install, pair the app, whole-home protection |
| `designs/` | Five distinct landing-page directions — browse `designs/index.html`, promote any one to the root |
| `CONTENT.md` | Single source of truth for copy, commands, and product facts |

## Editing rules

- Commands, ports, URLs, and setup steps live in `CONTENT.md` and must match
  the real repos — update it first, then the pages.
- The kit is a teaser only (parts + $50, coming soon). No checkout, no fake
  forms, mailto CTA until there's a real store.
- Keep the honest-limitation copy (streaming in-video ads aren't DNS-blockable)
  visible on every page that makes a blocking claim.
