# Testing

Manual verification steps for TES Map - Roscrea exports and packages.

## 🧪 Testing Philosophy

This project has **no automated tests**. All verification is manual, performed by the maintainer during the release process. The testing strategy focuses on visual correctness, format compliance, and in-game functionality.

## ✅ Pre-Release Verification Checklist

### 1. Source Asset Integrity

| Check | Method | Pass Criteria |
|-------|--------|---------------|
| XCF opens without errors | Open in GIMP | No missing layer errors, no corruption warnings |
| Layer structure intact | Inspect Layers panel | Expected groups present: Base Terrain, Labels, Icons, Borders, Adjustments |
| No flattened layers | Check layer count | > 10 layers (typical for this project) |
| Dimensions correct | Image → Image Properties | 4096 × 4096 px |

### 2. DDS Export Verification

| Check | Tool | Pass Criteria |
|-------|------|---------------|
| File opens | GIMP / DDS Viewer / texconv | No error loading |
| Format correct | DDS Viewer → Header | DDS, BC3/DXT5, mipmaps present |
| Mipmap count | DDS Viewer → Mip Levels | 13 levels (4096 down to 1) |
| Base dimensions | DDS Viewer → Level 0 | 4096 × 4096 |
| Alpha channel | DDS Viewer → Alpha | Non-zero in transparent areas (water, borders) |
| Colour space | Visual compare with XCF | Matches at 100% zoom |
| No compression artefacts | Visual inspect 100% zoom | No blocky artefacts on smooth gradients |
| File size reasonable | `ls -lh` | ~14–15 MB for full mip chain |

**Recommended DDS Viewers:**
- Linux: `texconv` (from DirectX-Tools), `ddsview` (AUR), GIMP
- Windows: DirectX Texture Tool, Paint.NET with DDS plugin
- Cross-platform: [Khronos KTX-Software](https://github.com/KhronosGroup/KTX-Software) tools

### 3. PNG Export Verification

| Check | Tool | Pass Criteria |
|-------|------|---------------|
| File opens | Any image viewer | No error |
| Dimensions | Image properties | 4096 × 4096 |
| Lossless | Compare with XCF | Pixel-perfect match (minus layer effects) |
| Alpha channel | Viewer alpha preview | Transparency where expected |
| File size | `ls -lh` | 8–12 MB typical |

### 4. Mod Archive Verification

| Check | Method | Pass Criteria |
|-------|--------|---------------|
| Archive opens | `7z l archive.7z` | Lists all files without error |
| Structure correct | `7z l archive.7z` | Matches BAIN/FOMOD layout |
| DDS included | `7z l archive.7z` | `textures/maps/roscrea.dds` present |
| FOMOD files present | `7z l archive.7z` | `fomod/ModuleConfig.xml`, `fomod/info.xml` |
| info.xml version | Extract and view | Matches release version |
| ModuleConfig valid | Extract and view | Well-formed XML, references correct paths |
| Archive size | `ls -lh` | ~15–16 MB (DDS dominates) |

**Expected Archive Listing:**
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

### 5. In-Game Verification (Optional but Recommended)

| Check | Method | Pass Criteria |
|-------|--------|---------------|
| Mod installs | MO2 / Vortex → Install | No errors, appears in mod list |
| Mod enables | Check plugin list | Texture loads (no ESP needed) |
| Map displays | Open map in-game (M key) | Roscrea map visible, correct orientation |
| No purple textures | Visual inspect | No missing texture fallback (purple/black checkerboard) |
| No flickering | Move camera | Stable at all zoom levels |
| Mipmaps work | Zoom in/out on map | Smooth transitions, no popping |
| Alpha works | Water, borders | Transparent where expected |

## 🔍 Regression Checks

When modifying the source asset, verify:

- [ ] Existing labels/icons/borders still render correctly
- [ ] No new visual artefacts introduced
- [ ] Colour balance consistent with previous version
- [ ] All layer groups still organised logically
- [ ] File size of XCF hasn't grown excessively (indicates unused data)

## 📝 Test Documentation

Record test results in release notes:

```
## Release v1.2.3 - Testing Notes
- DDS Export: ✅ BC3, 13 mip levels, 4096×4096, 14.6 MB
- PNG Export: ✅ 4096×4096, 9.2 MB
- Archive: ✅ BAIN/FOMOD structure valid, 15.1 MB
- In-Game: ✅ Map displays correctly, no purple textures, mipmaps smooth
- Mod Manager: ✅ Installs and enables via MO2 2.5.1
```

## 🚫 Known Limitations

| Limitation | Impact | Mitigation |
|------------|--------|------------|
| No automated visual diff | Manual comparison only | Side-by-side at 100% zoom |
| No format validator in CI | Relies on maintainer diligence | Checklist above |
| Single hardware test | May miss GPU-specific issues | Test on integrated + discrete if possible |
| No OBSE/plugin testing | Not applicable (texture only) | N/A |

## 🔗 Related Documents

- [Build and Deployment](build-and-deployment.md) — Release process including these checks
- [Configuration](configuration.md) — Export settings that affect test criteria
- [Data Model](data-model.md) — Expected formats and structures