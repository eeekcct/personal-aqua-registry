# personal-aqua-registry

## `aqua.yaml`

```yaml
checksum:
  enabled: true

registries:
  - type: standard
    ref: v4.471.0
  - name: eeekcct
    type: github_content
    repo_owner: eeekcct
    repo_name: personal-aqua-registry
    ref: <registry-tag>
    path: registry.yaml

packages:
  - name: eeekcct/wsx
    registry: eeekcct
    version: <wsx-version>
```

## `aqua-policy.yaml`

```yaml
registries:
  - type: standard
    ref: semver(">= 3.0.0")
  - name: eeekcct
    type: github_content
    repo_owner: eeekcct
    repo_name: personal-aqua-registry
    ref: semver(">= 0.0.1")
    path: registry.yaml

packages:
  - registry: standard
  - registry: eeekcct
```

```powershell
aqua policy allow
```

For a private repository, set `AQUA_GITHUB_TOKEN` or `GITHUB_TOKEN`.

## Download verification

Use a registry tag (or commit SHA) containing these verification settings in
`<registry-tag>` above. Existing configurations pinned to an older registry tag
will not receive them automatically.

With `checksum.enabled: true` in your `aqua.yaml`, aqua checks each downloaded
archive against the release's SHA256 checksum manifest. Commit the generated
`aqua-checksums.json` alongside `aqua.yaml`, and review checksum changes when
updating package versions. Registry checksum definitions alone do not enable
this consumer-side setting. An unsigned checksum manifest checks integrity; it
does not by itself authenticate the publisher.

SLSA provenance verification is also configured for:

- `eeekcct/kreseal`: v0.1.4 and later.
- `eeekcct/vtag`: v0.0.3 and later.
- `eeekcct/wsx`: all published versions (starting with v0.0.1).

For these versions, aqua verifies the archive against the provenance and the
expected application repository and release tag. Missing or invalid provenance
causes installation to fail. Older kreseal and vtag releases have no published
provenance, so only checksum verification is available for them; this fallback
is limited to those older versions.

Aqua automatically downloads its SLSA verifier when needed. This requires extra
network access for the verifier and provenance verification (including Sigstore
services). Do not disable verification to work around a verification failure.
These settings verify artifact origin and integrity, not whether the application
is free of vulnerabilities.

See aqua's [checksum documentation](https://aquaproj.github.io/docs/reference/security/checksum/)
and [Cosign/SLSA documentation](https://aquaproj.github.io/docs/reference/security/cosign-slsa/).
