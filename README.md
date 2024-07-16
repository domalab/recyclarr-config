# Sonarr and Radarr Configuration

This repository contains the configuration files for Sonarr and Radarr, optimized for high-quality media collection with a focus on compatibility with the Sonos Arc sound system.

## Table of Contents

1. [Overview](#overview)
2. [Files](#files)
3. [Quality Profiles](#quality-profiles)
4. [Custom Formats](#custom-formats)
5. [Audio Configuration](#audio-configuration)
6. [Recyclarr Integration](#recyclarr-integration)
7. [Maintenance](#maintenance)
8. [Troubleshooting](#troubleshooting)

## Overview

This configuration is designed to automate the process of acquiring high-quality TV shows and movies, with a particular emphasis on audio formats compatible with the Sonos Arc sound system. It uses Recyclarr to sync settings from TRaSH Guides, ensuring up-to-date and optimized configurations.

## Files

- `sonarr.yml`: Configuration file for Sonarr (TV shows)
- `radarr.yml`: Configuration file for Radarr (movies)
- `recyclarr.yml`: Configuration file for Recyclarr, which syncs settings with Sonarr and Radarr

## Quality Profiles

Both Sonarr and Radarr use three main quality profiles:

1. **Maximum**: Highest quality, preferring remux and full Blu-ray rips
2. **Optimized**: High quality, balancing size and quality
3. **HD Only**: Focuses on 1080p content

Sonarr has an additional **Anime** profile for anime content.

## Custom Formats

Custom formats are used to fine-tune media selection. Key categories include:

- HDR and Dolby Vision preferences
- Release group tiers
- Unwanted formats (e.g., 3D, BR-DISK)
- Repack/Proper handling

## Audio Configuration

The audio configuration is optimized for the Sonos Arc sound system, prioritizing:

1. Dolby Atmos (DD+ ATMOS)
2. Dolby Digital Plus (DD+)
3. Dolby Digital (DD)

Other formats like DTS and TrueHD are de-prioritized but still allowed if no better option is available.

## Recyclarr Integration

Recyclarr is used to automatically sync quality definitions, custom formats, and other settings from TRaSH Guides. The `recyclarr.yml` file configures this integration for both Sonarr and Radarr.

## Maintenance

To keep your configuration up-to-date:

1. Regularly run Recyclarr to sync the latest settings from TRaSH Guides
2. Periodically check TRaSH Guides for new recommendations or changes
3. Update your `sonarr.yml` and `radarr.yml` files if new custom formats or quality profiles are introduced

## Troubleshooting

If you encounter issues:

1. Verify that Recyclarr is running correctly and syncing settings
2. Check Sonarr and Radarr logs for any errors related to quality profiles or custom formats
3. Ensure that the YAML syntax in your configuration files is correct
4. Compare your settings with the latest TRaSH Guides recommendations

For persistent issues, consult the Sonarr, Radarr, or Recyclarr documentation and community forums.

---

This configuration is based on TRaSH Guides and community best practices. Always refer to the official documentation for Sonarr, Radarr, and Recyclarr for the most up-to-date information.