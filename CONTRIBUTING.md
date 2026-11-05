# Contributing to TES Map - Roscrea

This document covers the guidelines and processes for contributing to this project, including how to report issues, suggest enhancements, submit code changes, and follow project standards.

## 📑 Table of Contents

- [How to Contribute](#-how-to-contribute)
  - [Reporting Issues](#reporting-issues)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Code Contributions](#code-contributions)
    - [Prerequisites](#prerequisites)
    - [Development Setup](#development-setup)
    - [Making Changes](#making-changes)
    - [Pull Request Guidelines](#pull-request-guidelines)
  - [Code Style](#code-style)
  - [Testing](#testing)
  - [Documentation](#documentation)
- [Code of Conduct](#-code-of-conduct)
- [Security](#-security)
- [License](#-license)
- [Recognition](#-recognition)
- [Getting Assistance](#-getting-assistance)

## 🤝 How to Contribute

### Reporting Issues

- Search existing issues first.
- Use the issue templates if available.
- Provide clear reproduction steps.
- Include environment details.

### Suggesting Enhancements

- Check the roadmap and existing discussions.
- Explain the use case and expected behaviour.
- Consider implementation complexity.

### Code Contributions

#### Prerequisites

- [GIMP](https://gimp.org) or another editor compatible with XCF files.

#### Development Setup

```bash
# Clone the repository
git clone https://github.com/hmlendea/tes-map-roscrea.git
cd tes-map-roscrea

# Open the source file
# Open Roscrea.xcf in GIMP or your preferred XCF-compatible editor
```

#### Making Changes

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make your changes on separate layers when practical.
4. Export the final texture in the target format required by your mod package.
5. Commit with clear and descriptive messages.
6. Push to your fork.
7. Open a Pull Request.

#### Pull Request Guidelines

- Target the `master` branch.
- Keep PRs focused and atomic.
- Revise documentation if applicable.
- Ensure exported assets are valid and packaged correctly.

### Code Style

Follow the project's coding standards:
- Keep pull requests focused and consistent with the existing style.
- Apply modifications on separate layers when practical.

### Testing

No automated tests exist for this project. Verify exported assets manually.

### Documentation

- Revise relevant docs for changes.
- Follow the documentation style guide.
- Preview changes locally if possible.

## 📋 Code of Conduct

This project follows the [Code of Conduct](./CODE_OF_CONDUCT.md).

## 🔒 Security

For the security policy, supported versions, vulnerability reporting, and disclosure process, see [SECURITY.md](./SECURITY.md).

This project is a static map artwork asset with no runtime component, executable code, or network services. The security policy addresses supply-chain integrity of the distributed asset and responsible disclosure.

## 📄 License

By contributing, you agree that your contributions will be licensed under the GNU General Public License v3.0 or later.

## 🙏 Recognition

Contributors are recognized in the GitHub contributors list.

## ❓ Getting Assistance

- Open an issue on GitHub: https://github.com/hmlendea/tes-map-roscrea/issues
- Check existing discussions and documentation first.
- Consider funding the project: https://hmlendea.go.ro/funding