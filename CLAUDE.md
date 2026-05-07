# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This repo is **configuration only** — no code, no build, no tests. It feeds [Recyclarr](https://recyclarr.net), a CLI that syncs quality definitions, custom formats, and quality profiles from [TRaSH Guides](https://trash-guides.info) into Sonarr (TV) and Radarr (movies).

The whole config is tuned for one playback target: **Apple TV 4K → Sonos Arc**. Every score in the YAML files exists to push releases toward formats that path can decode losslessly, and away from ones it can't.

## Files

- `recyclarr.yml` — top-level Recyclarr config. Points at the local Sonarr/Radarr instances and pulls the per-app config from `includes/`. Uses `!secret sonarr_url` / `!secret sonarr_apikey` style references — the actual values live in a sibling `secrets.yml` (gitignored, not in this repo).
- `includes/sonarr.yml` — Sonarr quality profiles + custom format scoring.
- `includes/radarr.yml` — Radarr equivalents. Also includes movie-specific custom formats (release groups, streaming services, movie versions).

## Commands

There is no build/test/lint pipeline in-repo. Recyclarr runs externally:

```sh
recyclarr sync          # apply configs to Sonarr + Radarr
recyclarr sync sonarr   # one app only
recyclarr sync --preview  # dry-run, show what would change
```

Recyclarr expects `recyclarr.yml` and `secrets.yml` in the working directory (or `~/.config/recyclarr/`).

## Architectural notes for editing scores

A few things that aren't obvious from a single file:

**Custom format `trash_ids` are NOT shared between Sonarr and Radarr.** The same logical format (e.g. "DD+ ATMOS") has a different ID in each app's section of TRaSH Guides. When adjusting an audio/HDR format, change *both* `includes/sonarr.yml` and `includes/radarr.yml`, and look up each ID independently — copying an ID across files is a bug.

**Two profiles, mirrored across both apps:**
- `AppleTV-Optimized` — 4K-first, score_set `sqp-1-2160p`, upgrades up to Bluray-2160p.
- `HD Only` — 1080p ceiling, score_set `default`.
Whatever you change usually needs to apply to both profiles in both files (4 places).

**Audio scoring is the load-bearing logic.** Sonos Arc + Apple TV 4K can decode DD+ Atmos, DD+, DD; everything else (TrueHD/Atmos, DTS variants, OPUS) is heavily negative-scored to *block* matches, not just deprioritize them. The score scale used here:
- `+8000 / +6000 / +4000` — preferred audio (DD+ Atmos / DD+ / DD)
- `-5000` — ambiguous (e.g. undefined ATMOS container)
- `-8000 / -10000` — block (DTS family, TrueHD, OPUS)
- `+2500 / +2200 / +2000` — DV / HDR10+ / HDR boosts
- `+5000` — 2160p resolution preference (AppleTV-Optimized only)
- `+1500` — 1080p preference (HD Only only)
- `+1500` — premium release group tiers
- `+500` — special editions / proper releases
- `-1000` — unwanted (3D, BR-DISK, LQ, x265-HD, upscaled)

Don't invent new score magnitudes — fit changes into this scale or you'll perturb the relative ordering.

**`assign_scores_to: []`** (empty list) is intentional in `radarr.yml` for the Remux tiers — it explicitly opts out of scoring those for both profiles. Don't "fix" empty lists.

**Radarr-only sections:** movie versions (Criterion, IMAX, etc.), release-group tiers, streaming-service tags, Repack/Proper, and Uncensored live only in `radarr.yml`. Sonarr doesn't carry the equivalent set here.

## TRaSH Guide IDs

When adding a format, get the ID from TRaSH Guides directly (https://trash-guides.info) — *the Sonarr page for Sonarr edits, the Radarr page for Radarr edits*. The inline `# DD+ ATMOS` style comment next to each ID is the only label; keep it accurate when adding entries or future edits will reference the wrong format.
