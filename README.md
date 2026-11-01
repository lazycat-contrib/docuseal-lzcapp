# DocuSeal LazyCat community package

Upstream https://github.com/docusealco/docuseal (AGPL-3.0), 3.3.4. Package `community.lazycat.app.docuseal`, min OS 1.6.0 (needed for `run_as`), amd64, mirror delivery, community (喵喵) store only.

Single container. The upstream compose wires PostgreSQL plus Caddy, but its Rails `database.yml` already falls back to SQLite whenever `DATABASE_URL` is empty, and the image sets `WORKDIR=/data/docuseal`. So this package deliberately sets **no** `DATABASE_URL`, lets SQLite live at `/data/docuseal/db.sqlite3`, and binds `/lzcapp/var/data:/data` — the database, templates and signed PDFs persist together with no second container.

The image runs as uid/gid 2000, so `run_as: "2000:2000"` maps the persistent directory owner (mutually exclusive with `setup_script`).

No account is pre-seeded: no `deploy_params.yml`, no default admin. The first admin is created in the browser on first visit. `FORCE_SSL=false` because the LazyCat entry already terminates HTTPS.

Not device-tested: first admin creation, template editing, signing flow, PDF rendering, large documents, and persistence across restarts.
