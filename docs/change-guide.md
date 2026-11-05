# Change Guide

How to modify the TES Map - Roscrea asset safely and create releases.

## 🎯 Guiding Principles

1. **Never flatten the source** — Always work on separate layers in `Roscrea.xcf`
2. **Preserve non-destructive edits** — Use adjustment layers, masks, layer groups
3. **Test exports visually** — Verify at 100% zoom before packaging
4. **Document changes** — Update version, changelog, release notes
5. **Follow the release process** — [Build and Deployment](build-and-deployment.md)

## 🛠️ Common Modification Tasks

### Adding/Updating Labels

1. Open `Roscrea.xcf` in GIMP
2. Navigate to **Labels** layer group
3. Select appropriate sub-group (Region Names, Settlement Names, Geographic Features)
4. Create new text layer or edit existing
5. Use **Oblivion map font style**: Serif, slightly curved, dark brown/black with subtle glow
6. Position carefully — avoid overlapping icons or borders
7. Save XCF

### Adding/Updating Icons

1. Open `Roscrea.xcf` in GIMP
2. Navigate to **Icons** layer group
3. Select appropriate sub-group (Cities, Dungeons, Points of Interest)
4. Create new layer or edit existing
5. Use consistent icon style: Simple shapes, single colour, ~32×32 px at 4K
6. Position on pixel grid for crisp rendering
7. Save XCF

### Adjusting Terrain/Colour

1. Open `Roscrea.xcf` in GIMP
2. Navigate to **Base Terrain** or **Adjustments** layer group
3. For terrain: Edit Landmass, Water, Height Shading layers directly
4. For colour grading: Modify Adjustment layers (Curves, Levels, Colour Balance)
5. **Do not merge** adjustment layers — keep them live
6. Save XCF

### Modifying Borders

1. Open `Roscrea.xcf` in GIMP
2. Navigate to **Borders** layer group
3. Edit Political or Administrative sub-layers
4. Use paths (vectors) for clean, scalable borders
5. Stroke path on pixel-aligned layer
6. Save XCF

## 🔄 Safe Editing Workflow

```
1. Backup current XCF (git commit or copy)
2. Open Roscrea.xcf in GIMP
3. Create new layer/group for your changes
4. Make edits on new layer(s)
5. Toggle visibility to compare before/after
6. Save XCF
7. Export DDS + PNG (see Build and Deployment)
8. Visual verification (see Testing)
9. If satisfied: commit XCF, proceed to release
10. If not: iterate or revert
```

## 📝 Versioning Guidelines

| Change Type | Version Bump | Example |
|-------------|--------------|---------|
| Visual fix (typo, single pixel) | Patch | 1.2.3 → 1.2.4 |
| New labels/icons, minor adjustments | Patch | 1.2.3 → 1.2.4 |
| Significant visual changes | Minor | 1.2.3 → 1.3.0 |
| New region coverage, major redesign | Minor | 1.2.3 → 1.3.0 |
| Dimension change, format change | Major | 1.2.3 → 2.0.0 |

**Commit Message Format:**
```
type(scope): brief description

Details if needed.

Version: X.Y.Z
```

Types: `feat`, `fix`, `style`, `refactor`, `docs`, `chore`

## 🚀 Release Checklist

Before creating a release:

- [ ] XCF committed with descriptive message
- [ ] DDS exported with correct settings (BC3, mipmaps, sRGB)
- [ ] PNG exported for reference
- [ ] Visual verification passed (100% zoom, alpha, colours)
- [ ] Mod archive created with correct structure
- [ ] `info.xml` version updated
- [ ] Archive tested (opens, structure valid)
- [ ] In-game test passed (if possible)
- [ ] Release notes written
- [ ] Checksums generated (SHA-256)

## 🔧 Troubleshooting Common Issues

| Issue | Cause | Fix |
|-------|-------|-----|
| Purple textures in-game | Wrong DDS format / missing mipmaps | Re-export with BC3 + full mip chain |
| Blurry text/icons | Not pixel-aligned / wrong interpolation | Align to pixel grid; use NoHalo scaling |
| Alpha not working | Alpha not exported / premultiplied | Enable alpha export; disable premultiply |
| Archive rejected by Nexus | Wrong structure / missing FOMOD files | Verify BAIN/FOMOD layout |
| Large XCF file size | Unused layers, large undo history | Delete unused layers; File → Clean Up |
| GIMP crashes on export | Corrupt layer / memory | Save as new XCF; restart GIMP; try export |

## 📚 Best Practices

### Layer Organisation
- Use **layer groups** for logical organisation
- Name layers descriptively (`Label: Bruma`, `Icon: City: Bruma`)
- Keep related elements in same group
- Lock background/reference layers

### Non-Destructive Editing
- Use **adjustment layers** (Colors → Curves/Levels/Color Balance as layers)
- Use **layer masks** instead of erasing
- Use **paths** for vectors (borders, roads) — stroke on separate layers
- Duplicate layers before destructive operations

### Export Hygiene
- Hide guide/reference layers before export
- Verify only intended layers are visible
- Export to staging directory, not repo root
- Keep export settings consistent (documented in [Configuration](configuration.md))

## 🔗 Related Documents

- [Build and Deployment](build-and-deployment.md) — Full release process
- [Configuration](configuration.md) — Export settings reference
- [Testing](testing.md) — Verification checklist
- [Data Model](data-model.md) — Asset formats and structures
- [Architecture Notes](architecture.md) — Pipeline overview