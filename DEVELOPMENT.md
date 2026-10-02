# Edit, preview, and publish your academic CV

Live website: <https://MAGNC.github.io/academic-cv/>

Your account's existing Pages domain is `www.mathming.ltd`. GitHub currently
redirects the address above to <http://www.mathming.ltd/academic-cv/>.

## Preview locally

This site uses HugoBlox, Hugo Extended, Go, Node.js, and pnpm. Hugo 0.162.0
is pinned for GitHub Actions in `hugoblox.yaml`. Use Node.js 22 or newer locally.
On this Mac, these tools are already installed.

From the project folder, install the dependencies once:

```sh
pnpm install --frozen-lockfile
```

Start the preview:

```sh
pnpm dev
```

Open <http://localhost:1313/>. Leave the terminal running while you edit.
Saving a file rebuilds the site and reloads the browser. Drafts appear in the
local preview. Press Ctrl+C to stop the server.

In VS Code, you can also select **Terminal → Run Task → Preview academic CV**.

## What to edit

| File or folder | Content |
| --- | --- |
| `content/_index.md` | Homepage sections and research introduction |
| `data/authors/me.yaml` | Name, biography, affiliation, links, education, and experience |
| `config/_default/params.yaml` | Site identity, theme, header, footer, and search |
| `config/_default/menus.yaml` | Navigation links |
| `content/publications/` | Publication entries |
| `content/events/` | Talks and events |
| `content/blog/` | News and blog posts |
| `content/slides/example/index.md` | Example presentation |
| `static/uploads/resume.pdf` | Downloadable CV; replace this file with your PDF |

Many entries still contain sample material from the starter template.
Replace the sample author details, publications, projects, and CV before
sharing the site as your completed academic profile.

Keep YAML indentation consistent: use spaces, not tabs. Content pages begin
with YAML front matter between `---` lines, followed by Markdown text.
For files copied into `static/`, omit `static/` from their URL. Use site-relative
links such as `uploads/resume.pdf` so they work under `/academic-cv/`.

## Check the public build

```sh
pnpm build
```

This generates the production site and its Pagefind search index in `public/`.
Drafts are excluded. Generated output and installed dependencies are ignored
by Git; publish the source files.

## Publish changes

Review your changes in VS Code's Source Control panel, commit the files you
want to publish, and select **Sync Changes**. Alternatively:

```sh
git status
git add content/_index.md data/authors/me.yaml
git commit -m "Update academic profile"
git push origin main
```

Adjust the `git add` paths to include the files you edited. Each push to `main`
starts the [Pages deployment workflow](https://github.com/MAGNC/academic-cv/actions/workflows/deploy.yml).
The public site updates after the workflow succeeds. Local preview changes
do not become public until you commit and push them.

The repository uses **Settings → Pages → Source: GitHub Actions**, as described
in the [Hugo GitHub Pages guide](https://gohugo.io/host-and-deploy/host-on-github-pages/).
The deployment supplies GitHub's Pages URL to Hugo, including `/academic-cv/`.

## If the preview does not start

- Run commands from this project folder, where `package.json` is located.
- Run `pnpm install --frozen-lockfile` if the Tailwind or Pagefind dependencies are missing.
- If port 1313 is in use, stop the other preview or use `pnpm dev --port 1314 --baseURL http://localhost:1314/`.
- If YAML parsing fails, check the named file and line in the error message.
- If GitHub deployment fails, open the failed step in the Actions workflow to read its error.

The project explicitly permits the Tailwind executable in Hugo's
[`security.exec.allow` configuration](https://gohugo.io/configuration/security/)
so HugoBlox can build its stylesheet.
