# personal-aqua-registry

Add this registry to `aqua.yaml`.

```yaml
registries:
  - name: personal
    type: github_content
    repo_owner: eeekcct
    repo_name: personal-aqua-registry
    ref: v0.1.0
    path: registry.yaml
```

For a private repository, set `AQUA_GITHUB_TOKEN` or `GITHUB_TOKEN`.
