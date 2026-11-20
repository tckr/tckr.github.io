# tuckerseverson.com: working agreements

A one-page personal site: Tucker's name and a LinkedIn link on dot grid paper that visitors can draw on.

## How it's hosted

- This repo is `tckr/tckr.github.io` on GitHub, served by GitHub Pages at https://tuckerseverson.com (the `CNAME` file sets the domain; don't delete it).
- **Pushing to `master` publishes the site.** There is no build step and no staging copy. A push is live in about a minute.
- The domain is registered at Porkbun, which also hosts the DNS. HTTPS comes from GitHub and renews itself.
- Everything in the repo is public, and every file outside a dot-folder is served on the site. Keep notes and tooling in `.claude/`, and never commit anything private.

## Workflow

- Make changes locally, preview them, and **push only when Tucker says to** ("push it", "ship it"). "Add" or "try" means local only.
- Preview with the `site` entry in `.claude/launch.json` (a static server on port 5281). Check changes there before asking to push.
- After a push, confirm the live page is serving the change (fetch it with a cache-busting query such as `?t=1`).
- Commit straight to `master`; there are no branches, tickets or pull requests here.
- Say plainly what was checked by eye, what was only checked by script, and what wasn't checked (phones and dark mode are the usual gaps).

## How the page works

Everything is in `index.html`: styles, markup and one script. No dependencies apart from the IBM Plex Mono web font.

- **Paper:** a canvas draws a dot at every grid corner and a rounded square for each coloured cell. Squares are 18px (12px on screens narrower than 600px) and are counted from the centre of the window.
- **Drawing:** pressing a square moves it to the next of nine colours, then back to blank. Dragging paints blank squares with the stroke's colour and bumps coloured ones to their next colour.
- **Scenes:** the Random button takes turns through generated scenes (`SCENES` and `SCENE_ORDER`): a mountain landscape that differs each time, three tiled floors, a world map, and a mosaic mountain lake (sky bands, two ranges, pale reflection, dark pines). A scene is rebuilt from its kind and seed, so it re-fits when the window is resized.
- **Saved in the visitor's browser** (`localStorage`): the current scene and their own edits on top of it (`paper-v5`), the theme choice (`paper-theme`), and whether the name is hidden (`paper-name`). Change the storage key if the format changes.
- **Background:** the soft gradient, dot strength and grid size were tuned by Tucker in a separate playground. Ask before changing them; apply new settings exactly as given.
- **Theme:** follows the system by default; colours are CSS variables defined for light and dark.
- **Controls:** a reset icon and a three-dot menu top right; the menu unfolds Random, Name and Theme.

## Link previews

- `preview.png` (1200×630) is what Messages, Slack and others show for a shared link. `apple-touch-icon.png` (180px, the detailed tile mountain) is the home-screen icon. `favicon.svg` and `favicon.ico` (16/32/48px) are a simpler 3×3 tile mountain that stays legible in a browser tab; don't replace them with a scaled-down copy of the big one. The tags are in the page's `<head>`.
- The preview is a picture of the real page taken with headless Chrome: light theme, a mountain scene, the name placed higher, the link and buttons hidden, at an 800×420 window and 1.5× scale. Remake it if the page's look changes much.
- Apps cache previews. Test a change with a fresh address such as `https://tuckerseverson.com/?v=2`.

## Data sources

- The world map outline comes from Natural Earth (public domain), reduced to a 256×128 grid and stored run-length encoded in `index.html`.
- City maps from OpenStreetMap were tried and dropped. Using OpenStreetMap data again would need a visible credit line.
