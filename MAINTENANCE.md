# Project maintainer's guide

This page sets out our best practice for writing code, creating packages, writing docs,
making releases, creating packages, etc.

If you want to contribute to an Agile project, see [Contributing](CONTRIBUTING.md) instead.


## Branches

* **`develop`**: The bleeding edge. Always a release candidate. You can make PRs to this branch.
* **`main`** or **`master`** (older projects): Always tested and ready to become a new version.
  Don't push directly to this branch; make a new branch and submit a pull request to `develop`
  instead.
* **`gh-pages`**: Holds the HTML documentation and is served by GitHub Pages. The source files
  are in the `docs` folder. Do not push to `gh-pages`, it is managed by GitHub Actions.
