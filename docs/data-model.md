# Data Model

Asset representations and data structures for the TES Map - Roscrea project.

## 📊 Asset Representations

### 1. Source Asset: `Roscrea.xcf`

| Property | Value |
|----------|-------|
| **Format** | GIMP XCF (native) |
| **Role** | Authoritative source — single source of truth |
| **Layers** | Organised in groups: Base Terrain, Labels, Icons, Borders, Adjustments |
| **Colour Space** | sRGB (GIMP default) |
| **Precision** | 32-bit floating point per channel (GIMP default) |
| **Dimensions** | 4096 × 4096 px (typical for Oblivion map textures) |
| **Version Control** | Tracked in Git (binary) |

**Layer Organisation (Typical):**
```
Roscrea.xcf
├── Base Terrain (layer group)
│   ├── Landmass
│   ├── Water
│   └── Height Shading
├── Labels (layer group)
│   ├── Region Names
│   ├── Settlement Names
│   └── Geographic Features
├── Icons (layer group)
│   ├── Cities
│   ├── Dungeons
│   └── Points of Interest
├── Borders (layer group)
│   ├── Political
│   └── Administrative
└── Adjustments (layer group)
    ├── Colour Grading
    ├── Contrast
    └── Vignette
```

### 2. Runtime Texture: `roscrea.dds`

| Property | Value |
|----------|-------|
| **Format** | DDS (DirectDraw Surface) |
| **Compression** | BC3 / DXT5 (alpha channel support) |
| **Mipmaps** | Full chain generated (down to 1×1) |
| **Colour Space** | sRGB |
| **Dimensions** | 4096 × 4096 px (base level) |
| **Alpha Channel** | Used for transparency (water, borders) |
| **Byte Alignment** | 4-byte aligned per mip level |

**Mipmap Chain:**
| Level | Dimensions | Size (approx) |
|-------|------------|---------------|
| 0 | 4096 × 4096 | 11 MB |
| 1 | 2048 × 2048 | 2.75 MB |
| 2 | 1024 × 1024 | 688 KB |
| 3 | 512 × 512 | 172 KB |
| 4 | 256 × 256 | 43 KB |
| 5 | 128 × 128 | 11 KB |
| 6 | 64 × 64 | 2.7 KB |
| 7 | 32 × 32 | 680 B |
| 8 | 16 × 16 | 170 B |
| 9 | 8 × 8 | 43 B |
| 10 | 4 × 4 | 11 B |
| 11 | 2 × 2 | 3 B |
| 12 | 1 × 1 | 1 B |
| **Total** | — | **~14.6 MB** |

### 3. Reference Texture: `roscrea.png`

| Property | Value |
|----------|-------|
| **Format** | PNG (Portable Network Graphics) |
| **Compression** | Lossless (DEFLATE) |
| **Mipmaps** | None (single image) |
| **Colour Space** | sRGB |
| **Dimensions** | 4096 × 4096 px |
| **Bit Depth** | 32-bit (RGBA) |
| **File Size** | ~8–12 MB (varies with content) |

### 4. Mod Archive Structure

**BAIN/FOMOD Package:**
```
Roscrea Map vX.Y.Z.7z (or .zip)
├── textures/
│   └── maps/
│       └── roscrea.dds
├── fomod/
│   ├── ModuleConfig.xml    # FOMOD installer configuration
│   └── info.xml            # Mod metadata (name, version, author, description)
└── readme.txt              # Installation notes, credits, license summary
```

**ModuleConfig.xml (FOMOD):**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="http://qconsulting.ca/fo3/ModConfig5.0.xsd">
  <moduleName>TES Map - Roscrea</moduleName>
  <installSteps order="explicit">
    <installStep name="Main Texture">
      <optionalFileGroups order="explicit">
        <group name="Texture Resolution" type="selectExactlyOne">
          <plugins order="explicit">
            <plugin name="4K (4096×4096)">
              <description>Full resolution for modern hardware</description>
              <files>
                <folder source="textures" destination="textures" priority="0"/>
              </files>
            </plugin>
          </plugins>
        </group>
      </optionalFileGroups>
    </installStep>
  </installSteps>
</config>
```

**info.xml:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<fomod>
  <Name>TES Map - Roscrea</Name>
  <Author>hmlendea</Author>
  <Version>X.Y.Z</Version>
  <Website>https://github.com/hmlendea/tes-map-roscrea</Website>
  <Description>High-resolution map artwork of Roscrea in Oblivion style.</Description>
  <Groups>
    <element>Texture Resolution</element>
  </Groups>
</fomod>
```

## 🔄 Data Flow

```
Roscrea.xcf (source)
    │
    ├──▶ Export (GIMP) ──▶ roscrea.dds (runtime)
    │                         │
    │                         └──▶ Package ──▶ Mod Archive ──▶ Nexus Mods / GitHub Releases
    │
    └──▶ Export (GIMP) ──▶ roscrea.png (reference)
                              │
                              └──▶ Documentation, Previews, Web
```

## 📏 Invariants

| Invariant | Enforcement |
|-----------|-------------|
| XCF is sole authoritative source | Convention; documented in ARCHITECTURE.md |
| DDS uses BC3/DXT5 + full mip chain | Export settings documented in [Configuration](configuration.md) |
| PNG is lossless, no mipmaps | Export settings documented |
| Mod archive follows BAIN/FOMOD | Template files maintained by maintainer |
| No generated files in Git repo | .gitignore excludes *.dds, *.png, *.7z, *.zip |

## 🔗 Related Documents

- [Architecture Notes](architecture.md) — Pipeline overview
- [Configuration](configuration.md) — Export settings reference
- [Build and Deployment](build-and-deployment.md) — Step-by-step process