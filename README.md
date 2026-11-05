[![Donate](https://img.shields.io/badge/-%E2%99%A5%20Donate-%23ff69b4)](https://hmlendea.go.ro/funding)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://gnu.org/licenses/gpl-3.0)

# TES Map - Roscrea

High-resolution map artwork of Roscrea from The Elder Scrolls universe, in the visual style of
Oblivion's in-game map.

## 📑 Table of Contents

- [Features](#-features)
- [Usage](#-usage)
- [Installation](#-installation)
  - [Nexus Mods](#nexus-mods)
- [Development](#-development)
  - [Requirements](#requirements)
  - [Setup](#setup)
- [Contributing](#-contributing)
- [Security](#-security)
- [Architecture](#-architecture)
- [Support](#-support)
- [License](#-license)

## ✨ Features

- Lore-consistent map composition for Roscrea.
- Oblivion-style presentation suitable for modding and reference usage.
- Source project file included as `Roscrea.xcf` for further editing.

## 🚀 Usage

Install the mod package from Nexus Mods and use it in your Oblivion setup, or use the included
map asset as a reference in related Elder Scrolls modding projects.

## 📦 Installation

### Nexus Mods

[![Obtain it from Nexus Mods](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/nexus.png)](https://nexusmods.com/oblivion/mods/53055)

1. Download the archive from Nexus Mods.
2. Extract the contents into your Oblivion mod directory or mod manager staging directory.
3. Enable the mod using your preferred mod manager.

## 🛠️ Development

### Requirements

- [GIMP](https://gimp.org) or another editor compatible with XCF files.

### Setup

1. Open `Roscrea.xcf` in your image editor.
2. Apply your modifications on separate layers when practical.
3. Export the final texture in the target format required by your mod package.

## 🤝 Contributing

You are welcome to submit any suggestion, feedback, or modification to this project.

When doing so, please:
- Submit focused pull requests that conform to the existing code style
- Maintain your branch synchronised with `master`
- Revise the documentation when functionality changes
- Raise a new [issue](https://github.com/hmlendea/tes-map-roscrea/issues) for problems or suggestions

See the [Contributing Guidelines](./CONTRIBUTING.md) for details on how to report issues, suggest enhancements, and submit changes.

## 🔒 Security

For the security policy, supported versions, vulnerability reporting, and disclosure process, see [SECURITY.md](./SECURITY.md).

This project is a static map artwork asset with no runtime component, executable code, or network services. The security policy addresses supply-chain integrity of the distributed asset and responsible disclosure.

## 🛡️ Privacy and Data

For the detailed description of how the application handles privacy and personal data, see the [Privacy Statement](./PRIVACY.md).

This project is a static map artwork asset with no runtime component. No personal data is collected, processed, stored, or transmitted by the project itself. Distribution occurs through Nexus Mods, which operates under its own privacy policy.

## 📜 Code of Conduct

This project follows the [Code of Conduct](./CODE_OF_CONDUCT.md).

## 💝 Support

Discovered a problem or have a suggestion? [Open an issue](https://github.com/hmlendea/tes-map-roscrea/issues)!

If you find this project useful, consider [funding it](https://hmlendea.go.ro/funding) or starring ⭐️ it on GitHub!

[![Donate](https://raw.githubusercontent.com/hmlendea/readme-assets/master/donate_generic.png)](https://hmlendea.go.ro/funding)

## 🏗️ Architecture

This project follows a **single-source asset pipeline** architecture. The authoritative source is `Roscrea.xcf` (GIMP native format), which preserves layers, masks, and non-destructive edits. All downstream artefacts — exported textures (DDS for Oblivion, PNG for reference) and distribution packages — are derived manually from this source.

```mermaid
flowchart TD
    Source[Roscrea.xcf\n(Authoritative Source)] --> Export[Manual Export\n(GIMP)]
    Export --> Texture[Exported Texture\n(DDS/PNG)]
    Texture --> Package[Mod Package\n(Archive + Metadata)]
    Package --> Nexus[Nexus Mods]
    Package --> GitHub[GitHub Releases]
```

Key architectural boundaries:
- **Source Layer:** `Roscrea.xcf` — sole authoritative representation; all edits occur here
- **Export Boundary:** Manual, maintainer-driven; no automated build pipeline
- **Distribution Layer:** Packaged archives on Nexus Mods and GitHub Releases; immutable once published

The project has no runtime component, executable code, or network services. It is a static artwork asset consumed by The Elder Scrolls IV: Oblivion via mod managers.

See [ARCHITECTURE.md](./ARCHITECTURE.md) for the complete architecture documentation including system context, data architecture, interfaces, deployment, compatibility contracts, and design constraints.

## 📜 License

This project is licensed under the GNU General Public License v3.0 or later.
See [LICENSE](./LICENSE) for full details.
