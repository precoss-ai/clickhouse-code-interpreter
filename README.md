# clickhouse-code-interpreter (unofficial builds)

CI builds of [ClickHouse/code-interpreter](https://github.com/ClickHouse/code-interpreter)
published to GHCR as **multi-arch** images (`linux/amd64` + `linux/arm64`).

**Not affiliated with ClickHouse.** Images are stock upstream Dockerfiles at a
pinned commit; this repo only holds the build workflow and pin.

## Images

| Image | GHCR |
|---|---|
| API | `ghcr.io/protom-gmbh/codeapi-api` |
| Worker | `ghcr.io/protom-gmbh/codeapi-worker` |
| Sandbox runner | `ghcr.io/protom-gmbh/codeapi-sandbox-runner` |
| File server | `ghcr.io/protom-gmbh/codeapi-file-server` |
| Tool call server | `ghcr.io/protom-gmbh/codeapi-tool-call-server` |
| Egress gateway | `ghcr.io/protom-gmbh/codeapi-egress-gateway` |
| Package init | `ghcr.io/protom-gmbh/codeapi-package-init` |

Tags:

- `sha-<12>` — immutable tag from the upstream commit (preferred)
- `latest` — moves with the pin on `main`

Each tag is a multi-arch manifest list. Clients pick `amd64` or `arm64`
automatically.

```bash
docker pull ghcr.io/protom-gmbh/codeapi-api:sha-4b72e9d01654
docker buildx imagetools inspect ghcr.io/protom-gmbh/codeapi-api:sha-4b72e9d01654
```

**Visibility:** org GHCR packages are created **private**. GitHub provides no API
to flip org package visibility — after the first successful publish of a *new*
package name, open Package settings → Change visibility → Public (one-time).

## Upstream pin

[`UPSTREAM_SHA`](UPSTREAM_SHA) is the single source of truth.

To bump:

1. Edit `UPSTREAM_SHA` to the new ClickHouse/code-interpreter commit.
2. Merge to `main` (or run **Build and publish** via `workflow_dispatch`).
3. Pin the new `sha-<12>` tags (or digests from the Actions summary) in your
   cluster Helm values.

## License

Upstream is Apache-2.0. This repository’s workflow/docs are also Apache-2.0.
See [ClickHouse/code-interpreter](https://github.com/ClickHouse/code-interpreter)
for NOTICE and third-party terms.
