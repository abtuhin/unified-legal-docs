# Legal notes

Privacy policies, terms and other legal pages for all my apps, hosted for free
on GitHub Pages.

```
_config.yml          site name, owner, contact email, URL settings
_layouts/            page templates (you rarely need to touch these)
assets/style.css     styling (light + dark mode)
index.html           home page; lists every app automatically
einburgerung/         Einbürgerung app (German is the binding version, English a translation)
  de/privacy.md      -> /einburgerung/de/privacy/
  de/terms.md        -> /einburgerung/de/terms/
  de/imprint.md      -> /einburgerung/de/imprint/
  en/…               -> /einburgerung/en/…
```

The Einbürgerung app links to `https://abtuhin.github.io/legal-notes/einburgerung/{de|en}/{privacy|terms|imprint}/`
(`LEGAL_BASE_URL` in the app's `src/features/settings/legal.ts`). Don't rename these paths without updating the app.

## Add a new app

1. Create a new folder, e.g. `my-cool-app/`. The folder name
   becomes part of the URL, so use lowercase letters and hyphens.
2. In every file in the new folder, update the front matter at the top:
   ```yaml
   ---
   app: My Cool App        # display name; groups the docs on the home page
   title: Privacy Policy
   last_updated: 2026-11-18
   ---
   ```
3. Edit the text, then commit and push. GitHub rebuilds the site in about a minute.

To add another kind of document (EULA, refund policy, cookie policy, ...),
create a new `.md` file in the app's folder with the same front matter. It shows
up on the home page and in the "More from" links automatically.

Inside any document you can use `{{ site.owner }}`, `{{ site.contact_email }}`,
`{{ site.jurisdiction }}` (set in `_config.yml`) and `{{ page.app }}`.

## Publish on GitHub Pages (one-time setup)

1. Create a **public** repository on GitHub named `legal-notes`. GitHub Pages is
   free for public repos.
2. In `_config.yml`, set `url` to `https://<your-username>.github.io`. Keep
   `baseurl: "/legal-notes"`, or change it if you named the repo differently.
3. Push this folder:
   ```sh
   git init -b main
   git add .
   git commit -m "Initial legal pages"
   git remote add origin https://github.com/<your-username>/legal-notes.git
   git push -u origin main
   ```
4. On GitHub, open the repo, go to **Settings → Pages**, and under **Build and
   deployment** set *Source* to **Deploy from a branch**, *Branch* to `main`,
   folder `/ (root)`. Save.
5. After a minute or two the site is live at
   `https://<your-username>.github.io/legal-notes/`, and the links for each app are:
   - `https://abtuhin.github.io/legal-notes/einburgerung/de/privacy/`
   - `https://abtuhin.github.io/legal-notes/einburgerung/en/privacy/`

   Paste these into App Store Connect, the Google Play Console, and so on.

### Optional: custom domain (e.g. `legal.example.com`)

Under **Settings → Pages → Custom domain**, enter the domain. Then add a `CNAME`
DNS record that points `legal` to `<your-username>.github.io`. In `_config.yml`,
set `url: "https://legal.example.com"` and `baseurl: ""`.

## Preview locally (optional)

```sh
bundle install
bundle exec jekyll serve
# open http://localhost:4000/legal-notes/
```
