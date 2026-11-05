# Temporary household Google EXECUTE trial image

This owner-only build branch publishes a Core 2026.10.0 ARM64 image containing
the three version-specific Google Assistant module changes and a hash manifest.
It is separate from the upstream-review patch branch and is not an upstream PR.

The context contains public source only. It contains no household configuration,
database, backups, API credentials or device pairing information. The Dockerfile
verifies the source hashes and version before the workflow performs an isolated
startup check with no network or household config mounted.

The workflow publishes only after the startup check succeeds. Publication is not
deployment: appliance backup, config check, controlled image switch and rollback
remain separate operations. Anonymous registry access must be checked before the
appliance is pointed at this image.
