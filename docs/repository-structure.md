# Repository Structure

File and directory layout for the TES Map - Roscrea project.

## 📁 Root Directory

```
tes-map-roscrea/
├── CODE_OF_CONDUCT.md      # Community standards
├── CONTRIBUTING.md         # Contribution guidelines
├── LICENSE                 # GNU GPL v3.0 or later
├── PRIVACY.md              # Privacy statement
├── README.md               # Project overview and quick links
├── SECURITY.md             # Security policy
├── Roscrea.xcf             # Authoritative source asset (GIMP format)
├── docs/                   # Detailed documentation
│   ├── INDEX.md            # Master navigation
│   ├── architecture.md     # Complementary architecture notes
│   ├── build-and-deployment.md
│   ├── change-guide.md
│   ├── configuration.md
│   ├── data-model.md
│   ├── dependencies.md
│   ├── repository-overview.md
│   ├── repository-structure.md
│   ├── security.md
│   └── testing.md
└── .github/                # GitHub configuration (if present)
    └── workflows/          # CI/CD workflows (if any)
```

## 📄 File Descriptions

### Root Files

| File | Type | Description |
|------|------|-------------|
| `Roscrea.xcf` | Binary (GIMP) | **Authoritative source** — layered map artwork with masks, adjustment layers, and non-destructive edits. All modifications must be made here. |
| `README.md` | Markdown | Project overview, installation, usage, development, contributing, security, architecture, license. |
| `ARCHITECTURE.md` | Markdown | Complete architecture: system context, data architecture, interfaces, deployment, compatibility contracts, design constraints, extension points. |
| `SECURITY.md` | Markdown | Security policy: supported versions (Nexus Mods, GitHub Releases), vulnerability reporting via GitHub Security Advisories, disclosure policy, safe harbour, recognition. |
| `CONTRIBUTING.md` | Markdown | Guidelines for issues, pull requests, branch sync, documentation updates. References SECURITY.md. |
| `CODE_OF_CONDUCT.md` | Markdown | Community standards and enforcement procedures. |
| `PRIVACY.md` | Markdown | Data handling statement — no personal data collected by project; distribution via Nexus Mods under their policy. |
| `LICENSE` | Text | GNU General Public License v3.0 or later full text. |

### Documentation Directory (`docs/`)

| File | Description |
|------|-------------|
| `INDEX.md` | Master navigation linking all core and detailed documentation |
| `repository-overview.md` | High-level project summary, purpose, scope, architecture summary |
| `repository-structure.md` | This file — file and directory layout with descriptions |
| `architecture.md` | Complementary notes on asset pipeline, export process, distribution |
| `data-model.md` | Asset representations: XCF source, DDS/PNG exports, mod archive structure |
| `build-and-deployment.md` | Manual export, packaging, and release process |
| `configuration.md` | Export settings, GIMP version, compression parameters |
| `dependencies.md` | External dependencies: GIMP, Oblivion, Nexus Mods, GitHub |
| `testing.md` | Manual verification steps for exports and packages |
| `security.md` | Complementary security notes on supply-chain and asset integrity |
| `change-guide.md` | How to modify the asset safely and create releases |

## 🎯 Key Principles

1. **Single Source of Truth:** `Roscrea.xcf` is the only authoritative representation
2. **No Generated Files in Repo:** Exported textures (DDS, PNG) and mod archives are **not** committed — they are produced during release and published externally
3. **Documentation Co-location:** Core docs at root; detailed docs in `docs/`
4. **Cross-References:** All docs link to each other and to root documents