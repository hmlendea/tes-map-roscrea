# Security Notes

Complementary security documentation for the TES Map - Roscrea asset pipeline.

## 🔒 Security Scope

This project is a **static game mod asset** with no runtime component, executable code, network services, or data processing. The security policy addresses:

- **Supply-chain integrity** of the distributed asset
- **Asset authenticity** and tamper detection
- **Responsible disclosure** for any discovered issues

See [Root SECURITY.md](../SECURITY.md) for the complete security policy including supported versions, reporting process, disclosure policy, safe harbour, and recognition.

## 🎯 In-Scope Assets

| Asset | Risk | Mitigation |
|-------|------|------------|
| `Roscrea.xcf` (source) | Source tampering | Git history, signed commits (optional) |
| Exported DDS | Runtime substitution | Checksum verification by user |
| Mod Archive | Archive tampering | Nexus Mods moderation, GitHub Release signatures |
| Distribution Channels | Channel compromise | HTTPS, platform authentication |

## 🛡️ Supply-Chain Integrity

### Source Repository (GitHub)

- **Signed Commits:** Maintainer should use GPG-signed commits (`git commit -S`)
- **Branch Protection:** `master` branch protected; PR reviews required
- **Tag Signing:** Release tags signed (`git tag -s`)
- **Access Control:** Only maintainer has write access

### Distribution Channels

| Channel | Integrity Mechanism |
|---------|---------------------|
| **Nexus Mods** | Platform moderation; HTTPS download; file hashes displayed |
| **GitHub Releases** | Signed tags; HTTPS; `gh release` creates attested assets |

### Verification by Users

Users can verify asset integrity:

```bash
# Verify GitHub Release asset (if maintainer provides checksums)
sha256sum "Roscrea Map v1.2.3.7z"
# Compare with published checksum

# Verify Nexus Mods download
# Nexus displays SHA-1 on file page
```

## 🚫 Out-of-Scope

| Area | Reason |
|------|--------|
| Oblivion Runtime | Host game; not this project's responsibility |
| Mod Managers (MO2, Vortex) | Third-party tools; their own security |
| Nexus Mods Platform | Third-party platform; their own security |
| GitHub Platform | Third-party platform; their own security |
| User Systems | End-user environment; not controllable |

## 🔍 Asset Tampering Detection

### Indicators of Compromise

| Indicator | Detection |
|-----------|-----------|
| Unexpected file size | Compare with published checksums |
| Missing mipmaps | DDS viewer shows incomplete chain |
| Wrong compression | DDS viewer shows non-BC3 format |
| Visual anomalies | Purple textures, artefacts in-game |
| Archive structure mismatch | 7z listing differs from expected |

### Response

If tampering suspected:
1. **Do not install** the suspicious file
2. **Report** via GitHub Security Advisory (see [SECURITY.md](../SECURITY.md))
3. **Verify** against known-good source (GitHub Release, Nexus Mods)
4. **Re-download** from official channel

## 📋 Maintainer Security Practices

- Use GPG-signed commits and tags
- Verify exports visually before packaging
- Publish checksums (SHA-256) in release notes
- Keep GIMP and tools updated
- Use strong, unique credentials for Nexus Mods and GitHub
- Enable 2FA on all accounts

## 🔗 Related Documents

- [Root SECURITY.md](../SECURITY.md) — Complete security policy
- [Build and Deployment](build-and-deployment.md) — Release process with verification steps
- [Testing](testing.md) — Verification checklist
- [Architecture Notes](architecture.md) — Distribution layer boundaries