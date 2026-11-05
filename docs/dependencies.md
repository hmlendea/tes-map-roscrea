# Dependencies

External dependencies for the TES Map - Roscrea project.

## 📦 Runtime Dependencies (Mod Consumption)

| Dependency | Version | Role | Source |
|------------|---------|------|--------|
| **The Elder Scrolls IV: Oblivion** | Any (GOTY/Steam/GOG) | Host game consuming the texture | Bethesda |
| **Mod Manager** | MO2 2.5+ / Vortex 1.5+ | Stages and enables mod package | Community |
| **Oblivion Script Extender (OBSE)** | Not required | — | — |

**Note:** The mod is a texture replacer. No scripts, plugins (ESP/ESM), or OBSE are required.

## 🛠️ Build-Time Dependencies (Maintainer)

| Tool | Minimum Version | Recommended | Purpose | Installation |
|------|-----------------|-------------|---------|--------------|
| **GIMP** | 2.10.0 | 2.10.38+ | Edit XCF, export DDS/PNG | Flatpak, distro pkg, installer |
| **GIMP DDS Plugin** | 3.0.0 | 3.0.1+ | BC3/DXT5 + mipmap export | Bundled with GIMP |
| **7-Zip / p7zip** | 16.02 | 23.01+ | Create .7z mod archive | `apt install p7zip-full` / `brew install p7zip` |
| **Git** | 2.30 | 2.45+ | Version control, tagging | Distro pkg / installer |
| **GitHub CLI (`gh`)** | 2.0 | 2.50+ | Create GitHub Releases | `brew install gh` / `apt install gh` |

### GIMP DDS Plugin Verification

The DDS plugin must support:
- BC3 / DXT5 compression
- Full mipmap chain generation
- sRGB colour space
- Alpha channel export

**Test:** File → Export As → `test.dds` → verify options appear.

## 🌐 Distribution Platform Dependencies

| Platform | Role | Account Required | API/CLI |
|----------|------|------------------|---------|
| **Nexus Mods** | Primary distribution | Yes (free) | Web UI only (no official API for uploads) |
| **GitHub Releases** | Secondary distribution | Yes (free) | `gh release` CLI, REST API |

**Nexus Mods Notes:**
- Manual upload via web interface
- Moderation queue for new files (usually < 24h)
- No automated publishing from CI/CD

**GitHub Releases Notes:**
- Can be automated via `gh` CLI or GitHub Actions
- No moderation; immediate publication
- 2 GB file size limit per asset

## 📋 Mod Metadata Dependencies

| File | Schema | Validation |
|------|--------|------------|
| `info.xml` | FOMOD 5.0 (custom) | Manual review |
| `ModuleConfig.xml` | FOMOD ModuleConfig 5.0 | [XSD](http://qconsulting.ca/fo3/ModConfig5.0.xsd) |

**FOMOD Schema Reference:** http://qconsulting.ca/fo3/ModConfig5.0.xsd

## 🔗 Transitive Dependencies

| Dependency | Via | Notes |
|------------|-----|-------|
| **GTK 3** | GIMP | Linux: system package |
| **GLib** | GIMP | Linux: system package |
| **babl / GEGL** | GIMP | Colour processing, bundled |
| **zlib / libdeflate** | PNG, 7z | Compression, system library |
| **LZMA SDK** | 7z | LZMA2 compression, bundled |

## 📦 Dependency Management

| Aspect | Approach |
|--------|----------|
| **Version Pinning** | Documented in this file; not enforced by tooling |
| **Updates** | Manual; maintainer updates when needed |
| **Compatibility** | Tested manually during release |
| **Lock Files** | None (no package manager for these tools) |

## 🔄 Update Checklist

When updating any dependency:

- [ ] Verify GIMP still exports DDS with BC3 + mipmaps correctly
- [ ] Verify 7z creates valid archives Nexus Mods accepts
- [ ] Verify `gh` CLI creates releases correctly
- [ ] Test full release flow end-to-end
- [ ] Update version numbers in this document

## 🔗 Related Documents

- [Configuration](configuration.md) — Tool settings and versions
- [Build and Deployment](build-and-deployment.md) — Process using these tools
- [Architecture Notes](architecture.md) — Integration points