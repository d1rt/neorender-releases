# Neorender Releases

Public distribution repository for signed Neorender FW artifacts. It contains no product source code and is not consumed through the GitHub API by devices.

## Published objects

- `dev.json` — signed Dev channel manifest.
- `stable.json` — signed Stable channel manifest when a release is promoted.
- GitHub Release assets — immutable `neorender-fw-<version>-armv7.tar.gz` packages.

Devices read ordinary public HTTPS URLs. Every manifest is Ed25519-signed and binds product, channel, version, updater compatibility, architecture, package URL, SHA-256, size and release notes. SHA-256 is an integrity check; the signature is the origin guarantee.

## Publishing

1. Build and verify one release artifact with the private key held outside both repositories.
2. Publish the exact verified package as a GitHub Release asset.
3. Publish a signed `dev.json` referencing those exact bytes.
4. Complete device OTA, reboot, rollback and recovery QA.
5. Promote the already tested artifact by publishing a separately signed `stable.json`; do not rebuild it.

The release private key and access tokens must never be committed, uploaded as assets or copied to a Neorender device.
