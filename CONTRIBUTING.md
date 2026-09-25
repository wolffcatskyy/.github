# Contributing

Thanks for helping. This applies to every wolffcatskyy repo unless the repo has its own
`CONTRIBUTING.md`.

## Before you open an issue

- Search open and closed issues first.
- File it in the repo that owns the code. Bouncer problems go to
  [crowdsec-unifi-bouncer](https://github.com/wolffcatskyy/crowdsec-unifi-bouncer), installer
  problems to [crowdsec-unifi-suite](https://github.com/wolffcatskyy/crowdsec-unifi-suite),
  blocklist import problems to
  [crowdsec-blocklist-import](https://github.com/wolffcatskyy/crowdsec-blocklist-import).
  The awesome lists only take list changes.
- For UniFi-related bugs, include the device model, UniFi OS version and `ipset list -t`
  output. The issue form asks for these.
- Security problems: don't open a public issue. See [SECURITY.md](SECURITY.md).

## Pull requests

1. Fork, then branch from `main`.
2. Keep each PR to one change. Small PRs get reviewed faster.
3. Use [Conventional Commits](https://www.conventionalcommits.org/) for the PR title
   (`fix: ...`, `feat: ...`, `docs: ...`). Releases and changelogs are generated from them.
4. Run the repo's tests and linters locally. CI runs ShellCheck, yamllint and a link check.
5. Update docs and the README when behavior or config changes.
6. Don't add dependencies unless there's no reasonable way around them.

Target: every PR gets a first response within 7 days.

## Code style

- Shell: POSIX `sh` or Bash as the file already uses, `set -eu` where it fits, clean under
  ShellCheck. These scripts run on UniFi OS, so avoid tools that aren't on the device.
- Go: `gofmt`, `go vet`, `staticcheck`.
- Python: match the repo's existing tooling.
- LF line endings everywhere.

## AI-assisted contributions

Fine, as long as you've read and tested what you submit. The issue forms are structured so
you can paste them straight into an assistant; see
[ai-ready-issues](https://github.com/wolffcatskyy/ai-ready-issues).

## Code of conduct

By taking part you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).
