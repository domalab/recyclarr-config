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

- `recyclarr.yml`: Main Recyclarr configuration file that orchestrates the sync process
- `includes/sonarr.yml`: Sonarr-specific configuration file for TV shows
- `includes/radarr.yml`: Radarr-specific configuration file for movies

## Quality Profiles

Both Sonarr and Radarr use two main quality profiles:

1. **Sonos-Optimized**: Optimized for Sonos Arc + Apple TV 4K compatibility, supporting up to 4K with Dolby Vision/HDR, while prioritizing audio formats compatible with Sonos Arc (DD+ ATMOS, DD+, DD) and blocking incompatible formats (TrueHD, DTS)
2. **HD Only**: Focuses on 1080p content only, with broader audio format support including TrueHD and DTS

## Custom Formats

Custom formats are used to fine-tune media selection based on TRaSH Guides. Key categories include:

### Audio Formats
- **Preferred for Sonos Arc**: DD+ ATMOS (8000 pts), DD+ (6000 pts), DD (4000 pts)
- **Blocked for Sonos Arc**: TrueHD ATMOS, TrueHD, DTS-X, DTS-HD MA, DTS variants
- **HD Only Profile**: Supports all audio formats with appropriate scoring

### Video Quality
- **4K/HDR Optimization**: Dolby Vision HDR10/HDR10+ (2500 pts), other DV variants (2200 pts), HDR formats (2000 pts)
- **Resolution Preferences**: 4K (1800 pts), 1080p (800-1500 pts depending on profile)

### Release Quality
- **Premium Sources**: Top-tier release groups (1500 pts)
- **Streaming Services**: Major platforms like Netflix, Amazon Prime, Apple TV+ (100 pts)
- **Release Types**: Repacks/Proper releases (500 pts), special editions and remasters

### Blocked Content
- Poor quality releases (x265 HD, LQ releases, BR-DISK, extras) (-1000 pts)

## Audio Configuration

The audio configuration is specifically optimized for the Sonos Arc + Apple TV 4K setup:

### Sonos-Optimized Profile
1. **DD+ ATMOS** (8000 pts) - Highest priority, native Sonos Arc support
2. **DD+** (6000 pts) - Excellent quality, widely supported
3. **DD** (4000 pts) - Good fallback option
4. **Blocked Formats**: TrueHD ATMOS (-10000 pts), TrueHD (-8000 pts), DTS-X (-10000 pts), DTS variants (-8000 pts)

### HD Only Profile
- Supports all audio formats including TrueHD and DTS
- DD+ ATMOS (5000 pts), DD+ (1750 pts), DD (750 pts)
- TrueHD and DTS formats receive positive scores for this profile

The scoring system ensures that the Sonos-Optimized profile will completely avoid audio formats that cannot be properly processed by the Sonos Arc, while the HD Only profile maintains compatibility with a broader range of audio equipment.

## Recyclarr Integration

Recyclarr is used to automatically sync quality definitions, custom formats, and other settings from TRaSH Guides. The `recyclarr.yml` file configures this integration for both Sonarr and Radarr.

## Maintenance

To keep your configuration up-to-date:

1. Regularly run Recyclarr to sync the latest settings from TRaSH Guides
2. Periodically check TRaSH Guides for new recommendations or changes
3. Update your `includes/sonarr.yml` and `includes/radarr.yml` files if new custom formats or quality profiles are introduced
4. Monitor your media acquisitions to ensure the scoring is working as intended for your Sonos Arc setup

## Troubleshooting

If you encounter issues:

1. Verify that Recyclarr is running correctly and syncing settings
2. Check Sonarr and Radarr logs for any errors related to quality profiles or custom formats
3. Ensure that the YAML syntax in your configuration files is correct
4. Compare your settings with the latest TRaSH Guides recommendations

For persistent issues, consult the Sonarr, Radarr, or Recyclarr documentation and community forums.

---

This configuration is based on TRaSH Guides and community best practices. Always refer to the official documentation for Sonarr, Radarr, and Recyclarr for the most up-to-date information.