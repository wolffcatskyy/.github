# wolffcatskyy/.github

Shared defaults for every public repo under [wolffcatskyy](https://github.com/wolffcatskyy).

## What lives here

| File | Effect |
| --- | --- |
| `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `SUPPORT.md`, `.github/FUNDING.yml` | GitHub shows these on any repo that doesn't have its own copy. |
| `.github/ISSUE_TEMPLATE/` | Default issue forms for repos with no `ISSUE_TEMPLATE` folder of their own. |
| `.github/pull_request_template.md` | Default PR description for repos with no template of their own. |
| `.github/workflows/reusable-*.yml` | Reusable workflows that repos call with `uses:`. |

A repo-level file always wins. Bouncer-family repos (`crowdsec-unifi-bouncer`,
`crowdsec-unifi-suite`, `crowdsec-unifi-parser`) keep their own bug form with required
device model, UniFi OS version, `detect-device.sh` and `ipset list -t` fields. The default
bug form here uses the same field IDs and labels, so reports read the same across repos.

## Reusable workflows

Pin to a tag or commit SHA once one exists; `@main` is fine while this repo is young.

### Lint (ShellCheck, yamllint, LF line endings)

```yaml
jobs:
  lint:
    uses: wolffcatskyy/.github/.github/workflows/reusable-lint.yml@main
    with:
      shellcheck-ignore: sidecar
      yamllint-paths: .github/
```

### Link check (lychee)

```yaml
on:
  pull_request:
  schedule:
    - cron: "17 6 * * 1" # weekly
jobs:
  links:
    uses: wolffcatskyy/.github/.github/workflows/reusable-lychee.yml@main
```

### Releases (release-please)

```yaml
on:
  push:
    branches: [main]
permissions:
  contents: write
  pull-requests: write
jobs:
  release:
    uses: wolffcatskyy/.github/.github/workflows/reusable-release-please.yml@main
    with:
      release-type: simple # or python, go, node
```

Releases made with the default `GITHUB_TOKEN` don't trigger other workflows (for example a
tag-triggered Docker build). If a repo needs that, pass a token secret as `release-token`.

### Image signing (Cosign, keyless)

Call it after the image is pushed, passing the digest from `docker/build-push-action`:

```yaml
jobs:
  build:
    # ... outputs: digest: ${{ steps.push.outputs.digest }}
  sign:
    needs: build
    permissions:
      contents: read
      packages: write
      id-token: write
    uses: wolffcatskyy/.github/.github/workflows/reusable-cosign.yml@main
    with:
      image: ghcr.io/wolffcatskyy/crowdsec-sidecar
      digest: ${{ needs.build.outputs.digest }}
```

Verify a signed image:

```sh
cosign verify ghcr.io/wolffcatskyy/crowdsec-sidecar@sha256:... \
  --certificate-identity-regexp '^https://github.com/wolffcatskyy/' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com
```
