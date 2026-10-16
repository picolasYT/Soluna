# Releasing Soluna

Use semantic versions: `MAJOR.MINOR.PATCH`.

- **Patch** (`1.0.1`): compatible fixes and documentation updates.
- **Minor** (`1.1.0`): compatible features.
- **Major** (`2.0.0`): breaking changes.

## Release checklist

1. Start from an up-to-date `main` branch with a clean working tree.
2. Run the test suite:

   ```bash
   npm test
   ```

3. Bump the version. `npm version` updates `package.json` and
   `package-lock.json`, creates a version commit, and adds a matching Git tag:

   ```bash
   npm version patch
   # Use "minor" or "major" when appropriate.
   ```

4. Push the commit and tag:

   ```bash
   git push origin main --follow-tags
   ```

5. On GitHub, create a Release from the new `vX.Y.Z` tag. Summarize the
   user-visible changes and any upgrade notes.

6. If publishing the npm package is part of this release, publish only after
   confirming the package metadata and release contents:

   ```bash
   npm publish
   ```

For a first npm release, confirm the package name is available and the npm
account has publish access before running `npm publish`. Until then, users can
run Soluna directly from the GitHub checkout; see
[Getting started](getting-started.md#run-from-github).
