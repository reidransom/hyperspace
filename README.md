# Hyperspace by HTML5 UP

[html5up.net](https://html5up.net) | [@ajlkn](https://twitter.com/ajlkn)

Free for personal and commercial use under the CCA 3.0 license ([html5up.net/license](https://html5up.net/license))

## Development & content editing (Decap CMS)

This site is built with gojekyll and edited through Decap CMS running in local
backend mode — no hosting, auth, or git remote required. Decap's local proxy
(decap-server) is talked to by the admin UI only when the site is served on
localhost; edits are written straight to the working-tree files, which you then
commit with git.

**Requirements:**

- Node.js (for `npx decap-server`)
- gojekyll on your PATH

To edit content, run these in two terminals from the repo root:

1. Decap local backend proxy (listens on http://localhost:8081):

   ```sh
   npx decap-server
   ```

2. The site:

   ```sh
   gojekyll serve
   ```

Then open the `/admin/` path of the served site, e.g. http://localhost:4000/admin/
(use whatever host/port `gojekyll serve` prints).

**Notes:**

- Do NOT add `admin` to the `exclude:` list in `_config.yml` — that would also
  remove `/admin/` from `gojekyll serve`, which is exactly when you need it.
  `/admin/` is plain static files (no Node in production); decide whether to
  strip it from a production deploy at publish time.
- The `/admin/` content model lives in `admin/config.yml`.
- See `DEVELOPMENT.md` for the full rundown (what's editable, the `_data` `items:`
  wrapper, YAML comment caveat, and production/deploy guidance).

For the original HTML5 UP template notes, see below.

## About this template

So I've had the wireframe for this particular design kicking around for some time, but with all
the other interesting (and in some cases, semi-secret) projects I've been working on it took me
a little while to get to actually designing and coding it. Fortunately, things have eased up
enough for me to finaly get around to it, so I'm happy to introduce Hyperspace: a fun, blocky,
one-page design with a lot of color, a bit of animation, and an additional "generic" page template
(because hey, even one-page sites usually need an interior page or two). Hope you dig it :)

Demo images\* courtesy of Unsplash, a radtastic collection of CC0 (public domain) images
you can use for pretty much whatever.

(\* = not included)

AJ
aj@lkn.io | [@ajlkn](https://twitter.com/ajlkn)

## Credits

**Demo Images:**

- [Unsplash](https://unsplash.com)

**Icons:**

- [Font Awesome](https://fontawesome.io)

**Other:**

- [jQuery](https://jquery.com)
- [Scrollex](https://github.com/ajlkn/jquery.scrollex)
- [Responsive Tools](https://github.com/ajlkn/responsive-tools)
