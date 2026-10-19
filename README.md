# Ashworth & Vale Wealth Platform

A clickable, full-width prototype of a wealth-management desktop platform (dark theme, BNY-inspired).
34 screens: dashboard, clients/accounts/groups, account detail views, model portfolios,
trading tools, markets, alternatives, reports and workflows.

## Run it

It is plain static files, no build step. Serve the folder with any static server and open the printed URL:

```bash
python3 -m http.server 8080      # then visit http://localhost:8080
# or: npx serve .
```

Serve it over http rather than double-clicking the files: each screen loads itself through the runtime,
which browsers block on `file://`.
`index.html` is a launcher listing every screen; **Start at Dashboard** begins the click-through.

## Layout

```
index.html            launcher / screen index
screens/
  *.dc.html           one file per screen (Design Component format)
  support.js          the runtime every screen loads (React + the DC template engine)
```

- Screens link to each other with relative `href`s, so the sidebar, breadcrumbs, table rows and
  "Back to Wealth Platform" links all click through.
- Each screen fills the browser width. Wealth Platform screens scroll as a normal page with a sticky
  sidebar; the Trading, Reports and Fixed Income screens are app-shell layouts with their own inner scroll.
- State is per screen (theme toggle, collapsible nav, tabs, the Transfer Funds modal on account detail
  screens, the Eliza chat on the dashboard). It resets when you navigate.

## Editing

Each `.dc.html` is one HTML file: markup with `{{ }}` holes, plus a `class Component extends DCLogic`
script at the bottom holding state and handlers. Fonts load from Google Fonts (IBM Plex Sans/Mono, Archivo);
offline you get system fallbacks.

## Hosting on GitHub Pages

Settings → Pages → deploy from the `main` branch root. `.nojekyll` is included.
