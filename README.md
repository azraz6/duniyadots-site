# DuniyaDots — support and privacy site

The public pages behind the App Store listing for DuniyaDots:

| URL | Page |
|---|---|
| `/` | Product overview — the listing's **marketing URL** |
| `/support/` | Help and contact — the listing's **support URL** |
| `/privacy/` | Privacy policy — the listing's **privacy policy URL** |

Static HTML and one stylesheet. No build step, no framework, no JavaScript, no tracking.
It is the app's privacy policy rendered for the web, so it deliberately loads nothing from
anywhere else.

## Why the layout looks like this

Two constraints shaped it, both of which bit during setup:

- **Every link is relative.** Root-absolute paths such as `/style.css` resolve to the
  domain root, which on a project Pages site (`<user>.github.io/<repo>/`) is the wrong
  place — the stylesheet would 404 and the pages would render unstyled.
- **Each page is a directory with an `index.html`.** GitHub Pages serves only real files,
  so `/privacy` cannot map to `privacy.html`. A `privacy/index.html` does map, which gives
  a clean `/privacy/` URL and keeps working on any other static host.

`.nojekyll` stops Pages from running Jekyll over the site, which it otherwise does by
default. `vercel.json` is unused on Pages but keeps the site deployable to Vercel with the
same URLs.

## Updating

Edit the files, commit, push. Pages republishes in under a minute.

```bash
git add -A && git commit -m "Update privacy policy" && git push
```

If you change the privacy policy, change the **last updated** date on it, and update
`appstore/privacy-policy.md` in the main project so the two do not drift apart.

## Local preview

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000/>. The pages also respect the system light/dark setting.
