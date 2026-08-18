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

## Running Eternal in a container

`docker-compose.yml` in this repository runs Eternal without installing
anything on the host beyond Docker itself.

```bash
curl -O https://raw.githubusercontent.com/riddhimaaan/eternal-releases/main/docker-compose.yml
docker login ghcr.io -u YOUR-GITHUB-USERNAME
ETERNAL_UID=$(id -u) ETERNAL_GID=$(id -g) docker compose up -d
```

The image is published privately at `ghcr.io/riddhimaaan/eternal`. `docker
login` needs a GitHub token with access to it, which comes with your licence —
if the pull is refused, your access has not been granted or has lapsed.

Your data lives in `~/.eternal` on the host, so updates never touch it:

```bash
docker compose pull && docker compose up -d
```

The dashboard is then at http://127.0.0.1:9119, bound to this machine only.

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
