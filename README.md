# EVE Console — Documentation

Source for the EVE Console documentation site: **<https://docs.eveconsole.com/>**

Built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/). All pages live in [`docs/`](docs/); navigation is defined in [`mkdocs.yml`](mkdocs.yml).

## How it deploys

Cloudflare Workers builds this repo's **`main`** branch — `pip install -r requirements-docs.txt && mkdocs build` produces `./site`, then `npx wrangler deploy` (config in [`wrangler.jsonc`](wrangler.jsonc)) publishes it to `docs.eveconsole.com`. **Merge to `main` → live.**

This repo is intentionally separate from the application repo so documentation publishes independently of app releases.

## Editing

- Edit the Markdown in `docs/`; adjust the nav in `mkdocs.yml`.
- Preview locally: `pip install -r requirements-docs.txt && mkdocs serve`.
- CI (`.github/workflows/docs.yml`) runs `mkdocs build --strict` on pull requests to catch broken links or pages missing from the nav.

## Related

- Application: <https://github.com/kernoeve/EveConsole>
- Homepage: <https://eveconsole.com>
