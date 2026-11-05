# Architecture Notes

Complementary architecture documentation for the TES Map - Roscrea asset pipeline.

## 🔄 Asset Pipeline

The project follows a **single-source asset pipeline** with three stages:

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────────┐
│   Source Layer  │───▶│  Export Boundary │───▶│ Distribution Layer  │
│  Roscrea.xcf    │    │  Manual (GIMP)   │    │  Nexus / GitHub     │
└─────────────────┘    └──────────────────┘    └─────────────────────┘
```

### Stage 1: Source Layer (`Roscrea.xcf`)

- **Format:** GIMP native XCF
- **Contents:** Layered composition with base terrain, labels, icons, borders, adjustment layers, masks
- **Authority:** Sole source of truth — all edits occur here
- **Version Control:** Tracked in Git (binary, diff not meaningful)
- **Editing Practice:** Work on separate layers; use layer groups for organisation; preserve non-destructive edits

### Stage 2: Export Boundary (Manual, GIMP)

| Export Target | Format | Settings | Purpose |
|---------------|--------|----------|---------|
| Oblivion Runtime | DDS | BC3/DXT5 compression, mipmaps generated, sRGB | Game consumption |
| Reference / Web | PNG | Lossless, no mipmaps, sRGB | Documentation, previews |
| Archive Source | TGA (optional) | Uncompressed, no mipmaps | Intermediate for some tools |

**Export Process:**
1. Open `Roscrea.xcf` in GIMP
2. Hide/show layers as needed for target variant
3. File → Export As → choose format
4. Configure format-specific options (see [Configuration](configuration.md))
5. Verify visually at 100% zoom
6. Save to staging area (not committed to repo)

### Stage 3: Distribution Layer

**Mod Package Structure (BAIN/FOMOD):**
```
Roscrea Map/
├── textures/
│   └── maps/
│       └── roscrea.dds
├── fomod/
│   ├── ModuleConfig.xml
│   └── info.xml
└── readme.txt
```

**Publication Channels:**
| Channel | Role | Update Mechanism |
|---------|------|------------------|
| Nexus Mods | Primary | Manual upload via web UI |
| GitHub Releases | Secondary | Manual `gh release create` or web UI |

**Immutability:** Once published, archives are not modified. New versions = new uploads.

## 🏗️ Architectural Boundaries

| Boundary | Description | Enforcement |
|----------|-------------|-------------|
| **Source Integrity** | Only `Roscrea.xcf` is authoritative | Convention; no automated enforcement |
| **Export Reproducibility** | Same source → same export (given same settings) | Documented settings in [Configuration](configuration.md) |
| **Distribution Immutability** | Published archives never change | Platform policy (Nexus, GitHub) |
| **No Runtime Code** | Project contains no executable code | By design — static asset only |

## 🔗 Integration Points

| Integration | Type | Direction | Notes |
|-------------|------|-----------|-------|
| GIMP | Authoring Tool | Read/Write XCF | Version 2.10+ recommended |
| Oblivion | Host Game | Consumes DDS | Requires BC3/DXT5, mipmaps |
| Mod Managers (MO2, Vortex) | Deployment Tool | Consumes Archive | BAIN/FOMOD structure |
| Nexus Mods | Distribution Platform | Publish | Manual upload |
| GitHub Releases | Distribution Platform | Publish | Manual or CLI |

## 📐 Design Constraints

| Constraint | Rationale |
|------------|-----------|
| Single XCF source | Preserves editing flexibility; avoids sync issues between formats |
| Manual export | No CI/CD infrastructure; maintainer control over quality |
| DDS BC3 + mipmaps | Oblivion engine requirement for performance and quality |
| GPL v3+ license | Copyleft ensures derivatives remain free |
| No generated files in repo | Keeps repo small; avoids binary diff noise; source is truth |

## 🔄 Extension Points

| Extension | Description | Effort |
|-----------|-------------|--------|
| Additional Export Formats | TGA, KTX, WebP for other engines | Low — add export step |
| Automated Export Script | GIMP Python-Fu or CLI batch export | Medium — requires GIMP scripting |
| FOMOD Installer Options | Multiple texture resolutions, style variants | Medium — edit ModuleConfig.xml |
| Automated Release Workflow | GitHub Action to build and upload | High — requires GIMP headless or Docker |
| LOD Variants | Multiple resolution DDS for distant rendering | Medium — export at multiple sizes |

## 📚 Related Documentation

- [Root ARCHITECTURE.md](../ARCHITECTURE.md) — Complete formal architecture
- [Data Model](data-model.md) — Asset representations in detail
- [Build and Deployment](build-and-deployment.md) — Step-by-step release process
- [Configuration](configuration.md) — Export settings reference