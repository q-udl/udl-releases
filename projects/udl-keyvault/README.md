# UDL Key Vault Releases

Release catalog for UDL Key Vault.

Packages:

- `com.udl.keyvault.uat` — internal / UAT channel.
- `com.udl.keyvault` — production channel.

APK binaries are stored as assets in GitHub Releases in this repository. APK binaries are not committed to Git history.

Stable application update endpoints are served by the UDL Key Vault Cloudflare Worker:

- `https://udl-key-vault-auth.quality-udluthfi.workers.dev/v1/app-updates/android/internal`
- `https://udl-key-vault-auth.quality-udluthfi.workers.dev/v1/app-updates/android/production`
- `https://udl-key-vault-auth.quality-udluthfi.workers.dev/downloads/android/internal/latest.apk`
- `https://udl-key-vault-auth.quality-udluthfi.workers.dev/downloads/android/production/latest.apk`

Stable APK download endpoints return HTTP redirects to the exact immutable GitHub Release asset under `q-udl/udl-releases`.

Release metadata follows the shared UDL catalog contract:

- `latest-internal.json` is published only after a validated internal artifact exists.
- `latest-production.json` is published only after a validated production artifact exists.
- Immutable per-release metadata is stored under `releases/`.

A release metadata record must include the project, channel, version code/name, package name, release tag, APK filename, immutable GitHub Release asset URL, APK byte size, APK SHA-256, signing-certificate SHA-256, release notes, and publication timestamp.

Production signing material, passwords, tokens, encryption keys, and vault data must never be stored in this repository.

Do not publish placeholder `latest-*.json` records. A latest record becomes valid only after the matching APK has been built, signed, cryptographically verified, uploaded as an immutable GitHub Release asset, and approved for its channel.
