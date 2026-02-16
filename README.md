# personal-aqua-registry

## `aqua.yaml`

```yaml
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
