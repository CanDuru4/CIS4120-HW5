# Dependencies and maintenance

Moved out of the README.

- No GitHub Actions workflows. CodeQL runs as GitHub's default setup, not from a workflow file
  in this repository.
- [`.github/dependabot.yml`](../.github/dependabot.yml) checks npm dependencies weekly and batches
  them into two grouped PRs: `npm-minor-and-patch` for minor/patch bumps, and `npm-majors` for
  major bumps. Majors are grouped rather than ignored so that each one still gets a deliberate
  `npm ci && npm run build` check before it is merged.
- `package.json` carries an `overrides` block that pins transitive packages
  (`@humanfs/node`, `brace-expansion`, `nanoid`, `postcss`, `react-router`) to versions at or
  above their first patched release. Do not lower those floors without checking the
  corresponding advisories; `npm audit` should report zero vulnerabilities.
