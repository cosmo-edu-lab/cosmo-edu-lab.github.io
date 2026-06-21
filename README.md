# Cosmo-Edu-Lab — website source

Source of the project website, built with plain Jekyll (Markdown + a small
custom layout, no external theme dependency) and published via GitHub Pages.

## Structure

```
_config.yml          site settings, nav menu (edit nav: here to add/remove pages)
_layouts/default.html shared page shell (nav, footer, <head>)
_includes/            nav.html, footer.html
assets/css/style.css  all styling
assets/js/main.js     mobile-menu toggle (the only JS)
index.md              homepage
about.md, approach.md, app.md, team.md, contact.md
                       one page per menu item — edit these for content changes
```

Each page is plain Markdown with a small YAML front matter block at the top
(`layout`, `title`, `permalink`). You almost never need to touch HTML/CSS to
update content — just edit the relevant `.md` file.

## Local development (VS Code)

1. Install Ruby (>= 3.0) and Bundler if you don't have them already.
2. Open this folder in VS Code.
3. In the integrated terminal:
   ```bash
   bundle install
   bundle exec jekyll serve --livereload
   ```
4. Open `http://localhost:4000` — the page reloads automatically as you save
   files.

Recommended VS Code extensions: **Markdown All in One** (editing) and
**vscode-front-matter** (visual front-matter / page management for Jekyll —
optional but handy).

## Publishing

1. Set `url` and `baseurl` in `_config.yml` (see the comment above those
   fields — it depends on whether this is a `<user>.github.io` repo or a
   project repo).
2. Push to GitHub. In the repository settings, under **Pages**, set the
   source to the branch you're publishing from (e.g. `main`) — GitHub
   detects `_config.yml` and builds with Jekyll automatically. No GitHub
   Actions workflow is required.

## Adding images

Each page has commented-out `image:` / `image_alt:` fields at the top
(front matter). To give a page a header image:

1. Drop the file into `assets/images/` (recommended size ~1600×700px,
   landscape — it gets cropped to a fixed height automatically).
2. Uncomment the two lines and point `image:` to it, e.g.
   ```yaml
   image: "/assets/images/about.jpg"
   image_alt: "Students looking through a telescope"
   ```
3. Save — the image appears automatically below the page title.

You can also add images anywhere inside the body text of a page with
normal Markdown syntax:
```markdown
![Caption text](/assets/images/photo.jpg)
```

### Image beside text

To put an image next to a paragraph (text wraps around it, the most common
pattern for this kind of page), add `.float-left` or `.float-right` right
after the image:

```markdown
![Students analysing data](/assets/images/approach-1.jpg){: .float-left}

Activities use real astronomical datasets, from solar system objects to
galaxies to large-scale galactic networks. Students are guided to analyse
data according to their curriculum knowledge...
```

The image floats to that side (about 42% width) and the paragraph(s) that
follow wrap around it; it un-floats and stacks full-width automatically on
mobile. Alternate `.float-left` / `.float-right` between sections if you
want a left-right-left rhythm down the page. Headings, the `.grid`/`.columns`
blocks, and `<hr>` automatically clear the float, so you don't get a
trailing gap or overlap.

**Where to find images you can legally use** (relevant for an astronomy
project): NASA's image library (images.nasa.gov) is public domain; ESA/Hubble
(esahubble.org) and ESO (eso.org) release most images under Creative Commons
with attribution required — check the license on each individual image page.
For non-astronomy photos (classroom, students), Unsplash or Pexels offer
free-to-use stock photography.

## To do before launch

- Replace `github_repo` and `contact_email` placeholders in `_config.yml`
  with the real values.
- The install snippet on the App page (`app.md`) is a placeholder —
  replace with the library's actual install command.
- Add a real download link / release on the App page once available.
