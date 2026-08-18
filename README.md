# Eternal — releases

Version information for [Eternal](https://github.com/riddhimaaan/eternal).

This repository holds **metadata only**. The application source is private, and
this repo exists for one reason: a running copy of Eternal reads `latest.json`
to find out whether a newer version has been published.

## latest.json

```json
{
  "version": "0.17.0",
  "downloadUrl": "https://github.com/riddhimaaan/eternal-releases/releases",
  "notes": ["One short line per change, shown in the update window."]
}
```

| Field | Required | Meaning |
| --- | --- | --- |
| `version` | yes | The newest published version, e.g. `0.18.0`. Must be numbers separated by dots, optionally with a `v` prefix. |
| `downloadUrl` | no | Where a customer goes to get it. **Must start with `https://`** — the app refuses any other kind of link. Leave it out and the app sends people to this repo's Releases page. |
| `notes` | no | Short changelog lines. Up to 40, shown as bullet points. |

## Publishing a new version

1. Build the new version of the app.
2. Put the download wherever customers get it — your sales page, or a release
   on this repo if you are giving it away.
3. Edit `latest.json`: raise `version`, set `downloadUrl`, replace `notes`.
4. Commit and push to `main`.

Every running copy of Eternal picks the change up on its next check, and shows
a "new version available" message with that download link.

## What this does not do

Eternal never replaces itself. It reads this file, compares versions, and — if
yours is newer — offers the user a link. Downloading and installing is always
their choice.

## Note for paid distribution

Anything attached to a public release here can be downloaded by anyone, with no
way to see who took it. If Eternal is being sold, keep the build behind your
payment page and point `downloadUrl` there. This repo only ever needs to know
the version number.
