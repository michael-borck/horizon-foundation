# Horizon Foundation

Fictional community and not-for-profit employer in the WorkReady internship simulation. This repository contains its public website, careers/application pages, staff area and character content.

[WorkReady project home](https://github.com/michael-borck/workready-deploy) · [Content configuration](https://github.com/michael-borck/workready-deploy/blob/main/docs/configuration.md#content-sources-and-publication) · [Privacy](https://github.com/michael-borck/workready-deploy/blob/main/docs/privacy.md)

## Edit the site

| Path | Purpose |
|---|---|
| `brief.yaml` | Organisation profile and website context |
| `site/templates/`, `site/styles/`, `site/scripts/`, `site/assets/` | Site layout, presentation and browser behaviour |
| `content/employees/*.md` | Fictional employee biographies |
| `content/employees/*-prompt.txt` | Runtime character prompts; separate from biographies |
| `content/docs/` | Fictional policies and support materials, including grants, volunteers and program reporting |
| `content/jobs/`, `jobs.json` | Job authoring material and exported build input |
| `dist/` | Generated website published to GitHub Pages |

The workplace policies are teaching content. WorkReady's actual privacy and operating rules live in the project guides linked above.

## Build and publish

Requires Python 3 and [uv](https://docs.astral.sh/uv/). From this repository:

```bash
uv run --quiet --with pyyaml --with jinja2 --with markdown python3 site/build.py
```

Ensure `jobs.json` agrees with the canonical `workready-api/jobs/horizon-foundation.json` export. If the company-root copy is missing from a fresh checkout, copy that API export here before building. Editing `brief.yaml` or job Markdown does not regenerate the export.

Review source changes and generated `dist/`. [The Pages workflow](.github/workflows/pages.yml) uploads checked-in `dist/` on a push to `main`; it does not run the builder.

Use the [local console](https://github.com/michael-borck/workready-deploy/blob/main/console/README.md) for visual previews with production submissions blocked. Application/staff requests use the WorkReady API and shared portal session client. Test functional changes with the [isolated browser journey](https://github.com/michael-borck/workready-deploy/blob/main/docs/operations.md#checks-before-publishing).

Runtime job/persona changes also need an API image refresh. Biography edits alone do not change character prompts. Follow the [content publication rules](https://github.com/michael-borck/workready-deploy/blob/main/docs/configuration.md#content-sources-and-publication).

Licensed under the [MIT License](LICENSE).
