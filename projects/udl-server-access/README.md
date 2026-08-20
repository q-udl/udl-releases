# UDL Server Access Control Releases

Release catalog for `com.udl.serveraccess`.

Distribution follows the same two-channel contract used by UDL-CS:

- `internal`: UAT / release-candidate validation before production cutover.
- `production`: production-only artifacts after the Windows enforcement stage is approved for live use.

APK binaries are stored as assets in GitHub Releases in this repository. They are not committed to Git history.

Stable application download endpoints are served by the UDL Server Cloudflare Worker and return HTTP redirects to the exact immutable GitHub Release asset:

- `/downloads/android/internal/latest.apk`
- `/downloads/android/production/latest.apk`

The Worker also exposes channel manifests:

- `/v1/app-updates/android/internal`
- `/v1/app-updates/android/production`

UDL Server uses mandatory-only updates. For every active channel manifest, `minimumVersionCode` must equal `latestVersionCode`; there is no optional-update state.

Release metadata files use the same catalog shape already used by Warehouse Goods QC Log:

- `latest-internal.json`
- `latest-production.json`
- `releases/<releaseTag>.json`

A metadata record must contain the package name, version code/name, release tag, APK filename, immutable GitHub Release asset URL, byte size, APK SHA-256, signing-certificate SHA-256, release notes, and publication timestamp.

Production signing material is never stored in this repository. `latest-production.json` must not be published until the production artifact has passed cryptographic verification and the Server Access Control production-cutover gate.