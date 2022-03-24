# Project maintainer's guide

This page sets out our best practice for writing code, creating packages, writing docs, making releases, creating packages, etc.

If you want to contribute to an Agile project, see [Contributing](CONTRIBUTING.md) instead.


## Philosophy

Agile's repos should have the following characteristics when possible:

- Lightweight: as few dependencies as possible. If you only need one function from `scipy`, consider writing it in pure NumPy.
- Predictable: avoid depending on old or niche packages.
- Standard: use standard formats like CSV and PNG; don't invent new ones.
- Docstrings: write docstrings.
- Docs: write docs oriented around typical use-cases, not only the API.
- Tests: write tests.
- Google-style: we follow [PEP 8](https://peps.python.org/pep-0008/) and [Google's style](https://google.github.io/styleguide/pyguide.html), more or less. For example, we use Google-style docstrings.


## Branches

* **`develop`**: The bleeding edge. Always a release candidate. You can make PRs to this branch.
* **`main`**: Always tested and ready to become a new version. Don't push directly to this branch; make a new branch and submit a pull request to `develop` instead.
* **`gh-pages`**: Holds the HTML documentation and is served by GitHub Pages. The source files are in the `docs` folder. Do not push to `gh-pages`, it is managed by GitHub Actions.


## Testing

We use [`pytest`](https://docs.pytest.org/en/7.1.x/) to test our programs. (In one simple package we use `doctest`, and it's good to include doctest-like examples in your docstrings.)

Usually we add a script called `run_tests.py` to run the tests and explain anything else, like how to renew the test plot baselines. See our other repos.

Typically we use the `pytest-cov` plugin for test coverage and the `pytest-mpl` plugin if we need to test plotting output from `matplotlib`. In general, we try to avoid having plotting in our packages. For example, if a package produces `xarray` objects, we can lean on their plotting instead.


## Documentation

We use [Sphinx](https://www.sphinx-doc.org/en/master/) to build documentation with the [`furo`](https://github.com/pradyunsg/furo) theme. In general the index file is written in RST and most of the other documents are either Jupyter Notebooks or Markdown files.

Keep the build process as close as possible to Sphinx and what's in the actual project. It's tempting to use GitHub Actions for post-processing, etc, but then there's non-obvious stuff happening and the docs probably won't build on local. Sphinx is so powerful that you can really accomplish almost anything with its options and extensions.


## Continuous integration

Uses GitHub Actions.


## Build system

We use the minimal PEP 517/518-style approach. The easiest thing to do is probably to look at one of our existing packages, e.g. [snowfake](https://code.agilescientific.com/snowfake/), which is a nice, small example package.

In a nutshell, the build system should comprise:

- `pyproject.toml`
- `setup.cfg` &mdash; contains the project details.
- `setup.py` &mdash; should be very small.
- `requirements.txt` &mdash; should contain a single dot and nothing else (requirements go in `setup.cfg` andnowhere else).

The project should build with:

    python -m build

We usually provide at least three optional installations, which are useful for other developers and for the CI system:

- `docs` &mdash; Installs the required packages for documentation. For example, the docs likely need `sphinx` and `furo`.
- `test` &mdash; Installs the required packages for tests, e.g. `pytest`.
- `dev` &mdash; Installs the packages needed for docs and tests.


## Versioning

We use simple semantic versioning:

- Start at 0.1.0. The next bugfix goes to 0.1.1. The next point release goes to 0.2.0. 
- The first non-beta release is 1.0.0, then 1.2.0, etc.
- It's sometimes worth making a release candidate (e.g. if you've been monkeying with the build system or CI). In this case release, for example, 0.1.3rc0 and go up from there, 0.1.3rc1, etc. When you are ready to release, use 0.1.3. This avoids ending up with 0.1.3, 0.1.4, 0.1.5, etc, with no material changes other than 'not broken'.


## Other project files

Projects should always have:

- `LICENSE` &mdash; Apache 2.0 unless there's a reason not to use it.
- `CONTRIBUTING.md` &mdash; Have a look at another of our repos.
- `AUTHORS.md` &mdash; Use ORCID links when possible; invite contributors to add themselves.
- [`CITATION.cff`](https://citation-file-format.github.io/)

The `CODE_OF_CONDUCT.md` file is copied automatically from https://github.com/agilescientific/community.
