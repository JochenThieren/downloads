# _template

Copy this folder to `tools/<tool>/` to add a new tool, then:

1. Rename and fill in `README.md` (this file) with a short description + install notes.
2. Start `CHANGELOG.md`.
3. Leave `latest.json` as-is — the release workflow overwrites it from the actual
   published release. (The committed values are just a placeholder so the file exists.)

`<tool>` is the short key used everywhere: the folder name, the tag prefix
(`<tool>-vX.Y.Z`), and the `tool` field in `latest.json`. Keep it lowercase, no spaces
(e.g. `bingocaller`, `sportscoreboard`).
