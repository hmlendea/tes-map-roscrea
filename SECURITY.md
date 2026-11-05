# Security Policy

This project is a static map artwork asset for The Elder Scrolls IV: Oblivion modding. It contains no executable code, runtime components, or network services. The security policy addresses supply-chain integrity of the distributed asset and responsible disclosure of any issues affecting the asset or its distribution.

## 📑 Table of Contents

- [Supported Versions](#-supported-versions)
- [Reporting a Vulnerability](#-reporting-a-vulnerability)
- [Scope](#-scope)
- [Disclosure Policy](#-disclosure-policy)
- [Safe Harbour](#-safe-harbour)
- [Recognition](#-recognition)
- [Related Documentation](#-related-documentation)

## 🛡️ Supported Versions

Use this table to indicate which project versions currently receive security maintenance.

| Version | Distribution Channel | Supported |
|---------|--------------------|-----------|
| Latest version | Nexus Mods | ✅ |
| Latest version | GitHub Releases | ✅ |
| Latest version | Unofficial third-party distribution channels | ❌ |
| Preceding versions | Any distribution channel | ❌ |

## 🚨 Reporting a Vulnerability

Please do not disclose suspected vulnerabilities publicly before maintainers have had an opportunity to validate and remediate them.

To report a vulnerability:
- [GitHub Security Advisories](https://github.com/hmlendea/tes-map-roscrea/security/advisories)
- Contact the maintainers directly

## 📌 Scope

The original maintainers are not responsible for changes, modifications, or security issues introduced by downstream forks.

The subsequent report categories are in scope for this repository:
- Supply-chain integrity of the distributed XCF and exported texture assets
- Unauthorised modification of the asset on official distribution channels
- Licence compliance issues affecting the GPL v3 distribution

The subsequent categories are out of scope unless explicitly stated to the contrary:
- Runtime vulnerabilities (the project has no runtime component)
- Issues introduced by downstream modifications, repacks, or derivative works
- Vulnerabilities in the host game (The Elder Scrolls IV: Oblivion) or mod loaders
- Distribution-channel platform vulnerabilities (Nexus Mods, GitHub)

## 📢 Disclosure Policy

This project follows coordinated disclosure:
1. Vulnerabilities are investigated privately.
2. A remediation plan is prepared and validated.
3. Public disclosure is published after a fix, mitigation, or agreed risk decision is available.
4. Credit is attributed in accordance with reporter preference and project policy.

## 🧾 Safe Harbour

If your investigation is conducted in good faith, confined to authorised scope, and disclosed responsibly, the maintainers will not pursue action for policy-compliant activity.

## 🙏 Recognition

We appreciate responsible disclosure. Reporters who desire public attribution may be acknowledged in release notes, advisories, or a dedicated acknowledgements section.

## 🔗 Related Documentation

| Document | Scope |
|----------|-------|
| `docs/security.md` | Complementary security notes (supply-chain, asset integrity, tamper detection) |
| `docs/build-and-deployment.md` | Release process including verification steps |
| `docs/testing.md` | Verification checklist for exports and packages |