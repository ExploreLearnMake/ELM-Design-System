# ELM Design System

Shared branding and visual design system for Explore Learn Make (ELM), Gordon's personal brand. This is the single source of truth for colors, type, and logo usage so they're defined once here instead of re-decided in every project.

This repo is meant to be used **with Claude** — other projects (in the parent [Claude - Personal](../README.md) workspace) reference the files here for design consistency rather than duplicating brand assets or re-deriving color choices per project.

## Contents

| File / Folder | Purpose |
| --- | --- |
| [design-schema.md](design-schema.md) | The design system itself — color palette (light/dark modes + functional colors), typography, logo usage guidance, and an optional spacing scale. Includes WCAG contrast ratios and colorblind-simulation notes behind each color choice. |
| `Logos/` | Final logo/icon/favicon exports — SVG and PNG, black and white variants, multiple sizes. See the "Logo Usage" table in `design-schema.md` for which file to use where. |
| `ColorSchemes.af` | Affinity source file for the color palette. Not tracked in git (see below) — kept locally as the editable source behind the palette in `design-schema.md`. |

## How to use this in a project

- **Colors and type:** read `design-schema.md` and pull the hex values / token names directly — don't introduce new brand colors in a project without adding them here first, so the palette stays consistent across sites/apps.
- **Logos:** use the file already in `Logos/` that matches the placement (see the Logo Usage table for size/background guidance). Don't re-export or re-color the logo per project.
- **New asset needs:** if a project needs a brand asset that doesn't exist yet (e.g. a new export size, a letterhead, an email signature), log it in the parent workspace's `assets-inventory.md` scratchpad rather than creating a one-off in the project folder.

## Status

Typography sizes, keyboard focus-visible / disabled states, and logo minimum clear space are still open — see "Open Questions" at the bottom of `design-schema.md`.

## Git

This folder has its own independent git repository, separate from the parent `Claude - Personal` root repo (per that workspace's [git model](../README.md#git-model)). `ColorSchemes.af` (and other `*.af` Affinity source files) are gitignored — only the exported, finished assets in `Logos/` are tracked.
