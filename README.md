# gnoshcodes-site

The gnoshcodes home page, served at https://gnoshcodes.com by GitHub Pages from the `gh-pages` branch.
Source of truth for the brand: `gn0sh/gnoshcodes` `docs/company/`.

Colors, fonts and other design tokens live in one file, `tokens.css` at the site root, which every page loads
before its own CSS. It holds the house layer of the gnoshcodes design system (`gn0sh/gnoshcodes`
`docs/design-system/`); page CSS reads its role names (`--ink`, `--ground`, `--accent-ink`, ...).
