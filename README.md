# downloads

Public distribution point for Jochen Thieren's Windows tools.

**This repository holds no source code** — only short docs and a small manifest per
tool. The actual programs are attached to [**Releases**](../../releases), served over
GitHub's CDN. Source for the open-source tools lives in each tool's own repository.

## Tools

| Tool | Latest manifest | Source |
|---|---|---|
| _(add your first tool under `tools/`)_ | `tools/<tool>/latest.json` | private / own repo |

Each `tools/<tool>/latest.json` always points at that tool's current release
(version, file name, size, SHA-256, and a direct download URL).

## Download & verify

1. Download the installer from the tool's latest [Release](../../releases).
2. Check its integrity against the published checksum:

   ```powershell
   CertUtil -hashfile .\<file>.exe SHA256
   ```

   Compare the result to `sha256` in that tool's `latest.json` (or to
   `SHA256SUMS.txt` on the release). They must match.

> The installers are **not code-signed**, so Windows SmartScreen may warn the first
> time. The SHA-256 checksum is how you confirm the file is exactly what was published.

## How releases are organised

- One repository, many tools. A release belongs to a tool via its **tag**:
  `<tool>-vX.Y.Z` (e.g. `bingocaller-v1.0.1`).
- Each release carries the installer plus `SHA256SUMS.txt`.
- Because `releases/latest` is repository-wide (newest release of *any* tool), link
  to a tool's **`tools/<tool>/latest.json`** for its true latest — that's the stable
  pointer the website reads.

## Publishing a new release

The build happens in the tool's own (often private) repository; only the finished
binary is pushed here. From that repo's CI, or by hand:

```bash
gh release create "<tool>-v<version>" \
  dist/<Tool>-<version>-setup.exe SHA256SUMS.txt \
  --repo JochenThieren/downloads \
  --title "<Tool> <version>" \
  --notes-file notes.md
```

A workflow in this repo (`.github/workflows/update-manifest.yml`) then regenerates
`tools/<tool>/latest.json` from the published release automatically.
