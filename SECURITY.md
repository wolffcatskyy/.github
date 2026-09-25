# Security policy

## Reporting a vulnerability

Please report privately through GitHub: open the affected repo, go to the **Security** tab
and click **Report a vulnerability**. Don't open a public issue or discussion.

Include:

- the repo and version or commit
- what an attacker can do and what they need (network position, device access, config)
- steps or a proof of concept
- for UniFi tools, the device model and UniFi OS version

You'll get an acknowledgement within 7 days. Fixes ship as a normal release with a GitHub
Security Advisory, and reporters are credited unless they'd rather not be.

## Supported versions

Only the latest release of each repo gets security fixes. Upgrade before reporting if you
can.

## Scope

In scope: code, install scripts, container images and release artifacts published from
wolffcatskyy repos.

Out of scope: CrowdSec itself, UniFi OS and upstream blocklists. Report those to their
maintainers. Entries in the awesome lists point to third-party projects; report problems
with those projects upstream.
