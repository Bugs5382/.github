# .github 🔧

> 🔗 Shared config, profile and community-health files for Bugs5382 repositories.

## 📝 release-drafter.yml

[`.github/release-drafter.yml`](.github/release-drafter.yml) is the canonical
[release-drafter](https://github.com/release-drafter/release-drafter) config shared across
Bugs5382 repositories: the standard categories, the Conventional-Commit autolabeler, and the
version-resolver mapping. A repo's own `release-drafter.yml` drifts out of sync the moment one
repo's categories change and the others don't follow, so this repo holds one copy and every other
repo points at it instead of keeping its own.

Every published release here re-attaches the current `.github/release-drafter.yml` as a release
asset of the same name (`job-release-asset.yaml`), so a repo can pin to an exact version of the
shared config.

## 🔌 Extending it

[`Bugs5382/release-drafter-action`](https://github.com/Bugs5382/release-drafter-action) reads a
shared config from a release asset at a pinned tag (never a branch, and never a moving major/minor
tag) through its `extends` input:

```yaml
- uses: Bugs5382/release-drafter-action@v1
  with:
    extends: Bugs5382/.github@v1.0.0
```

Pin to a specific tag of this repo and bump it deliberately; `extends` checks the download against
the sha256 digest GitHub reports for the asset, so a tampered or wrong asset fails closed.

## 📂 Other contents

Standard GitHub community-health files (`CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `SECURITY.md`,
`SUPPORT.md`, `FUNDING.yml`) and issue/PR templates, inherited by any Bugs5382 repo that does not
provide its own.

## 📄 License

MIT. See [LICENSE](LICENSE).
