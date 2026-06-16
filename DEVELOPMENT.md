# Development & content editing

This site is a Jekyll port of the HTML5 UP "Hyperspace" template, built with
[jigyll](https://github.com/reidransom/jigyll). Editing the site's content
through a UI is **optional**: it's served by a separate [Decap CMS](https://decapcms.org/)
layer that you only need to run when you want it.

## Development

To work on the site — templates, styles, and the build — you only need
`jigyll` on your PATH. From the repo root:

```sh
# Serve with live rebuild (prints the host/port, e.g. http://localhost:4000/)
jigyll serve

# Or produce a static build in _site/
jigyll build
```

That's everything required to run, preview, and build the site. The CMS below
is not needed for development.

## Content editing (optional)

If you'd rather edit content in a UI than hand-edit the source files, the site
ships with [Decap CMS](https://decapcms.org/) in **local backend** mode. Decap's
local backend lets you edit content on your machine with no hosting,
authentication, or git remote. It runs a small proxy (`decap-server`) that the
admin UI talks to when the site is served on `localhost`; edits are written
straight to the working-tree files (you commit them yourself with git).

Run these in **two terminals** from the repo root:

```sh
# 1) Decap local backend proxy (listens on http://localhost:8081)
npx decap-server

# 2) The site
jigyll serve
```

Then open the admin UI at the `/admin/` path of the served site, e.g.
<http://localhost:4000/admin/> (use whatever host/port `jigyll serve` prints).

This adds one requirement beyond development: Node.js (for `npx decap-server`).

### What's editable

The CMS (`admin/config.yml`) exposes:

- **Pages** — `index.html` (home: intro / "what we do" / "get in touch" copy
  and buttons) and `generic.md` (heading, hero image, Markdown body).
- **Site data** — `_data/*.yml`: spotlights, features, contact details, and the
  main + sidebar navigation.
- **Site settings** — `_config.yml`: title, tagline, description, author, URLs,
  share image, copyright. (`plugins`/`exclude` are shown too so they survive a
  save — leave them alone unless you mean to change the build.)

`elements.html` is a static style reference and is intentionally not in the CMS.

#### Notes / gotchas

- **`_data` files use an `items:` wrapper.** Decap file collections need a
  mapping at the root of a file, so the list files (`spotlights`, `features`,
  `navigation_main`, `navigation_sidebar`) nest their array under `items:`.
  Templates loop over `site.data.<name>.items`.
- **Decap doesn't preserve YAML comments.** Saving `_config.yml` (or any data
  file) through the CMS will drop comments and may reorder keys. Values are
  preserved; the build is unaffected.

## Production / deploying the `/admin/` page

In a normal Decap setup, `/admin/` ships to production and is gated by an
authenticated git backend (git-gateway, GitHub, Gitea, ...). **This repo is
configured local-only**, so there is no working production backend — the
`backend:` block in `admin/config.yml` is a placeholder that's only ever used as
a fallback off `localhost`.

Because of that, **exclude `/admin/` from the production deploy** until a real
backend is wired up. Do this at publish time, not via `_config.yml`'s `exclude:`
(that would also hide it from local dev). For example, after a build:

```sh
jigyll build
rm -rf _site/admin        # or: rsync -a --exclude='admin' _site/ <target>
```

When you later add an authenticated backend, replace the placeholder `backend:`
block, stop excluding `/admin/`, and editors can manage content in production.
