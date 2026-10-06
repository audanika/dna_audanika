# Changelog

## Unreleased

### Removed

- Remove dna_translate layer

## 0.1.2 - 2026-10-01

### Changed

- Raise all topic layers to their current releases, among them `dna_gg`
0.6.0: `/gg-ticket` asks whether the ticket repos are picked
automatically or entered by hand, and the AI keeps
`.gg/publish_config.json` up to date, so `gg do commit` and
`gg do publish` start with a prefilled commit message, merge message and
version increment
- Raise `helix` to 1.9.0

## 0.1.1 - 2026-09-07

### Added

- Add the audanika identity, vscode overrides and prettier config

### Changed

- Put audanika in the copyright line
- Declare dna_scripts explicitly instead of relying on dna_gg
- Point the manifest at the new dna_gg and dna_scripts

## 0.1.0 - 2026-09-02

- First release. The audanika umbrella: every topic layer in one
dependency, with `dnaCopyrightHolder` set to
`Dr. Gabriel Gatzsche. All Rights Reserved.`, matching the header the
aud_ repos already carry. The one file the layer carries itself is the
proprietary `LICENSE`, which every audanika repo shares.
