# Build and Deployment

Manual export, packaging, and release process for TES Map - Roscrea.

## 🔄 Release Flow Overview

```
Edit XCF → Export Textures → Verify → Package Archive → Publish to Nexus Mods → Create GitHub Release
```

All steps are **manual and maintainer-driven**. No automated CI/CD pipeline exists.

## 📋 Prerequisites

| Tool | Version | Purpose |
|------|---------|---------|
| GIMP | 2.10+ | Edit XCF, export DDS/PNG |
| Archive Tool | 7-Zip / p7zip | Create .7z mod archive |
| Git | 2.x | Tag release, push to GitHub |
| GitHub CLI (`gh`) | 2.x | Create GitHub Release (optional) |
| Web Browser | — | Upload to Nexus Mods |

## 🛠️ Step-by-Step Process

### 1. Edit Source Asset

1. Open `Roscrea.xcf` in GIMP
2. Make modifications on **separate layers** (never flatten the source)
3. Use layer groups for organisation
4. Save `Roscrea.xcf`

### 2. Export Runtime Texture (DDS)

1. In GIMP: **File → Export As...**
2. Filename: `roscrea.dds`
3. Format: **DDS (DirectDraw Surface)**
4. **Export Options:**
   - Compression: **BC3 / DXT5** (supports alpha)
   - Generate Mipmaps: **Yes** (full chain)
   - Colour Space: **sRGB**
   - Alpha Channel: **Export** (if transparency used)
5. Click **Export**
6. Save to staging directory (e.g., `~/roscrea-release/staging/`)

### 3. Export Reference Texture (PNG)

1. In GIMP: **File → Export As...**
2. Filename: `roscrea.png`
3. Format: **PNG**
4. **Export Options:**
   - Compression Level: 9 (maximum)
   - Save Colour Values from Transparent Pixels: **No**
   - Interlacing: **None**
5. Click **Export**
6. Save to same staging directory

### 4. Visual Verification

| Check | Method |
|-------|--------|
| DDS loads correctly | Open in GIMP or DDS viewer; verify mipmaps present |
| Colours match source | Compare side-by-side at 100% zoom |
| Alpha channel works | Check transparency areas (water, borders) |
| No artefacts | Inspect edges, text, icons at multiple zoom levels |
| Dimensions correct | Verify 4096×4096 base level |

### 5. Create Mod Archive

**Directory Structure:**
```
staging/
└── Roscrea Map/
    ├── textures/
    │   └── maps/
    │       └── roscrea.dds
    ├── fomod/
    │   ├── ModuleConfig.xml
    │   └── info.xml
    └── readme.txt
```

**Steps:**
1. Create the directory structure above
2. Copy `roscrea.dds` to `textures/maps/`
3. Update `info.xml` with new version number
4. Verify `ModuleConfig.xml` is correct
5. Update `readme.txt` if needed
6. Create archive:
   ```bash
   cd staging
   7z a "Roscrea Map v1.2.3.7z" "Roscrea Map/"
   ```

### 6. Publish to Nexus Mods

1. Log in to [Nexus Mods](https://nexusmods.com)
2. Navigate to mod page: [Oblivion Mod 53055](https://nexusmods.com/oblivion/mods/53055)
3. Click **Add File** → **Upload File**
4. Select the `.7z` archive
5. Fill in:
   - Version: `1.2.3`
   - Category: `Main File` (or `Update` for subsequent versions)
   - Changelog: Brief description of changes
6. Submit for moderation (if required) or publish directly

### 7. Create GitHub Release

**Via GitHub CLI (recommended):**
```bash
# Tag the release
git tag -a v1.2.3 -m "Release v1.2.3: Updated map artwork for Roscrea"

# Push tag
git push origin v1.2.3

# Create release with archive
gh release create v1.2.3 \
  --title "TES Map - Roscrea v1.2.3" \
  --notes "Updated map artwork for Roscrea. See Nexus Mods page for details." \
  ~/roscrea-release/staging/"Roscrea Map v1.2.3.7z"
```

**Via Web UI:**
1. Go to GitHub repository → Releases → **Create a new release**
2. Tag: `v1.2.3` (create new)
3. Title: `TES Map - Roscrea v1.2.3`
4. Description: Release notes
5. Attach the `.7z` archive
6. Publish

### 8. Post-Release

1. Verify both Nexus Mods and GitHub Release are accessible
2. Update any external references (README badges, documentation links)
3. Announce in relevant communities if desired

## 📝 Versioning Scheme

| Format | Example | Meaning |
|--------|---------|---------|
| Semantic | `v1.2.3` | Major.Minor.Patch |
| Nexus Mods | `1.2.3` | Same, without `v` prefix |
| Archive | `Roscrea Map v1.2.3.7z` | Human-readable |

**Guidelines:**
- **Patch:** Visual fixes, minor adjustments, metadata updates
- **Minor:** New labels, icons, significant visual changes
- **Major:** Complete redesign, dimension changes, format changes

## 🔧 Troubleshooting

| Issue | Resolution |
|-------|------------|
| DDS not loading in Oblivion | Verify BC3/DXT5 compression, mipmaps generated, sRGB |
| Alpha not working | Ensure alpha channel exported; check DDS viewer |
| Archive rejected by Nexus | Verify BAIN/FOMOD structure; check file size limits |
| GitHub Release fails | Check `gh` auth (`gh auth status`); verify tag pushed |

## 🔗 Related Documents

- [Configuration](configuration.md) — Export settings reference
- [Data Model](data-model.md) — Asset formats and archive structure
- [Architecture Notes](architecture.md) — Pipeline overview