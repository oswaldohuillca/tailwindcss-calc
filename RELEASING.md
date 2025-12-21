# Release Guide

This guide explains how to release a new version of `tailwindcss-calc` to npm and GitHub.

## Prerequisites

### One-time Setup

1. **npm Account**
   - Create account at [npmjs.com](https://www.npmjs.com/)
   - Login locally: `npm login`

2. **GitHub Token** (for CI - optional)
   - Go to GitHub Settings → Developer settings → Personal access tokens
   - Create token with `repo` and `packages` permissions
   - Add as `NPM_TOKEN` in repository secrets

3. **Install changelogen**
   ```bash
   npm install -g changelogen
   ```

## Release Process

### Step 1: Make Changes

Follow conventional commit format:

```bash
# Features (minor bump)
git commit -m "feat: add new border utilities"

# Fixes (patch bump)
git commit -m "fix: resolve calc overflow issue"

# Breaking changes (major bump)
git commit -m "feat!: change base width default"
# or
git commit -m "feat: change API

BREAKING CHANGE: Base width now defaults to 1920px"

# Documentation (no version bump)
git commit -m "docs: update README examples"
```

### Step 2: Release

Choose the appropriate command based on your changes:

```bash
# Automatic version detection (recommended)
npm run release

# Or specify version type:
npm run release:patch   # 0.0.x - bug fixes
npm run release:minor   # 0.x.0 - new features
npm run release:major   # x.0.0 - breaking changes
```

### What Happens:

1. ✅ Analyzes commits since last release
2. ✅ Determines version bump automatically
3. ✅ Updates `CHANGELOG.md` with grouped changes
4. ✅ Updates version in `package.json`
5. ✅ Creates git commit: `chore(release): v1.0.0`
6. ✅ Creates git tag: `v1.0.0`
7. ✅ Pushes commit and tag to GitHub
8. ✅ Publishes package to npm
9. ✅ GitHub Action creates GitHub release (automatic)

### Step 3: Verify

1. **Check npm**: https://www.npmjs.com/package/tailwindcss-calc
2. **Check GitHub**: https://github.com/oswaldohuillca/tailwindcss-calc/releases
3. **Test installation**:
   ```bash
   npm install tailwindcss-calc@latest
   ```

## Manual Steps (if needed)

### Generate Changelog Only

```bash
npm run changelog
```

### Create GitHub Release Manually

```bash
npm run release:gh
```

### Publish to npm Manually

```bash
npm publish
```

## Troubleshooting

### Error: "Not logged in to npm"

```bash
npm login
```

### Error: "403 Forbidden"

- Check you're logged in with correct account
- Verify package name is available on npm
- Ensure you have publish permissions

### Error: "Git working directory not clean"

```bash
git status
git add .
git commit -m "chore: prepare for release"
```

### Error: "No commits since last release"

You need at least one commit since the last tag.

## Version Strategy

- **Patch (0.0.x)**: Bug fixes, performance improvements
- **Minor (0.x.0)**: New features, backward compatible
- **Major (x.0.0)**: Breaking changes, API changes

## Commit Types

| Type | Description | Version Bump |
|------|-------------|--------------|
| `feat` | New feature | Minor |
| `fix` | Bug fix | Patch |
| `perf` | Performance improvement | Patch |
| `refactor` | Code refactoring | Patch |
| `docs` | Documentation only | None |
| `style` | Code style/formatting | None |
| `test` | Tests only | None |
| `chore` | Maintenance tasks | None |
| `ci` | CI/CD changes | None |

Add `!` after type or `BREAKING CHANGE:` in body for major bump:
- `feat!: change API`
- `fix!: breaking fix`

## Tips

1. **Test locally first**: Run `npm run changelog` to preview changes
2. **Use descriptive commits**: Good commits make better changelogs
3. **Group related changes**: Make multiple commits for different features
4. **Review CHANGELOG**: Check `CHANGELOG.md` after release
5. **Verify npm package**: Install and test before announcing

## Resources

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Changelogen Documentation](https://unjs.io/packages/changelogen)
- [Semantic Versioning](https://semver.org/)

