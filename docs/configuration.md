# Configuration

Export settings, tool versions, and parameters for the TES Map - Roscrea asset pipeline.

## 🎨 GIMP Export Settings

### DDS Export (Oblivion Runtime)

| Setting | Value | Notes |
|---------|-------|-------|
| **Format** | DDS (DirectDraw Surface) | |
| **Compression** | BC3 / DXT5 | Required for alpha channel (transparency) |
| **Generate Mipmaps** | Yes (Full Chain) | Down to 1×1; Oblivion requires this |
| **Mipmap Filter** | Box / Linear | Box is faster; Linear is higher quality |
| **Colour Space** | sRGB | Oblivion expects sRGB textures |
| **Alpha Channel** | Export | Required for water, borders, feathered edges |
| **Premultiply Alpha** | No | Standard for game textures |
| **Normal Map** | No | This is a diffuse/albedo map |

**GIMP DDS Plugin Version:** 3.0.1+ (bundled with GIMP 2.10+)

### PNG Export (Reference / Web)

| Setting | Value | Notes |
|---------|-------|-------|
| **Format** | PNG | |
| **Compression Level** | 9 (Maximum) | Lossless; smaller file |
| **Interlacing** | None | Not needed for local/reference use |
| **Save Colour Values from Transparent Pixels** | No | Standard |
| **Save Background Colour** | No | Not applicable |
| **Save Gamma** | Yes | Preserves sRGB |
| **Save Resolution** | No | Not needed |
| **Save Creation Time** | No | Not needed |

### TGA Export (Optional Intermediate)

| Setting | Value | Notes |
|---------|-------|-------|
| **Format** | TGA | |
| **Compression** | None (Uncompressed) | Lossless, no artefacts |
| **Bit Depth** | 32-bit (RGBA) | Includes alpha |
| **RLE Compression** | No | Uncompressed preferred for intermediates |

## 🖥️ Tool Versions

| Tool | Minimum Version | Recommended | Purpose |
|------|-----------------|-------------|---------|
| **GIMP** | 2.10.0 | 2.10.38+ | XCF editing, DDS/PNG export |
| **GIMP DDS Plugin** | 3.0.0 | 3.0.1+ | DDS export with BC3/mipmaps |
| **7-Zip / p7zip** | 16.02 | 23.01+ | Mod archive creation (.7z) |
| **Git** | 2.30 | 2.45+ | Version control, tagging |
| **GitHub CLI (`gh`)** | 2.0 | 2.50+ | GitHub Release creation |

**GIMP Installation Notes:**
- Linux: `flatpak install flathub org.gimp.GIMP` or distro package
- Windows: Installer from gimp.org
- macOS: `brew install --cask gimp` or installer

**Verify DDS Plugin:**
1. Open GIMP
2. File → Export As → type `.dds` → should appear in format list
3. If missing: reinstall GIMP or install `gimp-dds` package separately

## 📐 Asset Dimensions

| Asset | Dimensions | Rationale |
|-------|------------|-----------|
| **Source (XCF)** | 4096 × 4096 px | Matches Oblivion map texture standard |
| **DDS Base Mip** | 4096 × 4096 px | Full resolution |
| **DDS Mip Chain** | Full to 1×1 | Oblivion engine requirement |
| **PNG Reference** | 4096 × 4096 px | 1:1 with source for accurate review |

**Alternative Resolutions (for FOMOD options):**
| Variant | Dimensions | Use Case |
|---------|------------|----------|
| 4K (Default) | 4096 × 4096 | Modern hardware, high VRAM |
| 2K | 2048 × 2048 | Mid-range hardware |
| 1K | 1024 × 1024 | Low VRAM, older systems |

*To create variants: Scale image in GIMP (Image → Scale Image) before export, using **NoHalo** or **LoHalo** interpolation.*

## 🗜️ Compression Parameters

### DDS BC3 / DXT5

| Parameter | Value |
|-----------|-------|
| Block Size | 4×4 pixels |
| Bits per Block | 128 bits (16 bytes) |
| Compression Ratio | 8:1 (vs uncompressed RGBA8) |
| Alpha Support | Explicit 8-bit alpha per block |
| Quality | Good for smooth gradients; visible banding on sharp alpha transitions |

### PNG DEFLATE

| Parameter | Value |
|-----------|-------|
| Algorithm | DEFLATE (zlib) |
| Compression Level | 9 (maximum) |
| Filter Type | Adaptive (per scanline) |
| Compression Ratio | 2:1 to 10:1 (content dependent) |

### 7z (LZMA2)

| Parameter | Value |
|-----------|-------|
| Algorithm | LZMA2 |
| Dictionary Size | 64 MB (default) |
| Word Size | 64 (default) |
| Solid Block | On (default) |
| Compression Level | 9 (Ultra) |

## 🎯 Colour Management

| Aspect | Setting |
|--------|---------|
| **Working Space (GIMP)** | sRGB (built-in) |
| **Source XCF Profile** | sRGB IEC61966-2.1 |
| **Export DDS Profile** | sRGB (no embedded ICC) |
| **Export PNG Profile** | sRGB (no embedded ICC) |
| **Monitor Calibration** | sRGB / 6500K / 2.2 gamma recommended |

**Note:** Oblivion does not perform colour management. Textures are interpreted as sRGB directly. Ensure GIMP is in sRGB mode (default).

## 📦 Mod Package Metadata

### info.xml (Required Fields)

| Field | Value | Example |
|-------|-------|---------|
| `Name` | Mod display name | `TES Map - Roscrea` |
| `Author` | Author name | `hmlendea` |
| `Version` | Semantic version | `1.2.3` |
| `Website` | Project URL | `https://github.com/hmlendea/tes-map-roscrea` |
| `Description` | One-line summary | `High-resolution map artwork of Roscrea in Oblivion style.` |

### ModuleConfig.xml (FOMOD)

| Element | Purpose |
|---------|---------|
| `moduleName` | Displayed in installer |
| `installSteps` | Ordered installation steps |
| `optionalFileGroups` | User choices (e.g., resolution) |
| `plugins` | File sets per choice |
| `files/folder` | Source→destination mapping |

## 🔧 Environment Variables (Optional)

| Variable | Purpose | Example |
|----------|---------|---------|
| `ROSCREA_STAGING` | Staging directory for exports | `/home/user/roscrea-staging` |
| `ROSCREA_RELEASES` | Output directory for archives | `/home/user/roscrea-releases` |

## 🔗 Related Documents

- [Build and Deployment](build-and-deployment.md) — Step-by-step process using these settings
- [Data Model](data-model.md) — Asset formats and structures
- [Architecture Notes](architecture.md) — Pipeline overview