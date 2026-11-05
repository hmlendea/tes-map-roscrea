# Repository Overview

High-level summary of the TES Map - Roscrea project.

## 🎯 Purpose

This repository hosts the source artwork and distribution assets for **TES Map - Roscrea**, a high-resolution map of Roscrea from The Elder Scrolls universe, rendered in the visual style of Oblivion's in-game map. The project is a static game mod asset with no runtime component, executable code, or network services.

## 📦 Scope

| Aspect | Description |
|--------|-------------|
| **Primary Asset** | `Roscrea.xcf` — GIMP native format preserving layers, masks, and non-destructive edits |
| **Exported Formats** | DDS (BC compressed, mipmapped) for Oblivion runtime; PNG for reference |
| **Distribution** | Packaged mod archives on Nexus Mods (primary) and GitHub Releases (secondary) |
| **Target Platform** | The Elder Scrolls IV: Oblivion via mod managers (MO2, Vortex) |
| **License** | GNU GPL v3.0 or later (copyleft applies to artwork and derivatives) |

## 🏗️ Architecture Summary

The project follows a **single-source asset pipeline**:

```
Roscrea.xcf (source) → Manual Export (GIMP) → DDS/PNG (textures) → Mod Package → Nexus Mods / GitHub Releases
```

- **Authoritative Source:** `Roscrea.xcf` — all edits occur here
- **Export Boundary:** Manual, maintainer-driven; no automated build pipeline
- **Distribution Layer:** Immutable packaged archives once published

## 👥 Audience

- **Maintainers:** Edit source, export textures, create releases
- **Mod Users:** Download and install via mod manager
- **Contributors:** Submit artwork modifications or suggestions

## 🔗 Related Documents

- [Architecture](../ARCHITECTURE.md) — Complete architecture documentation
- [Repository Structure](repository-structure.md) — File and directory layout
- [Data Model](data-model.md) — Asset representations and formats
- [Build and Deployment](build-and-deployment.md) — Export, packaging, release process