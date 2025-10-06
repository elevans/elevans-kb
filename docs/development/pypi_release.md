PyPi release
===

## PyPI release for Python only projects

### Remove project `dev` version and create a Git tag

1. Confirm the repository CI jobs are passing.
2. Remove the `dev0` label from the project version in the `pyproject.toml` or `setup.py` file.
3. Create a new commit with `Release version #.#.#`.
4. Tag the commit with `git tag #.#.#` where `#.#.#` is the version number.
5. Bump the project minor version number, add back the `dev0` to the version number and commit with "Bump to next development cycle".
6. Push the commits and push the tag. To push the tag use the following command: `git push origin 1.10.0`. With out this command tags are stored only locally.

### Publish the package on PyPI

1. Checkout the appropriate version tag.
    - For example: `git checkout 1.10.0`
2. Build the Python package with `python -m build` (_Note_: You can install `build` from PyPi with `pip install build`).
3. Upload to PyPi with `twine upload dist/*`

## PyPI release for Rust + PyO3 projects

1. Confirm the repository CI jobs are passing.
2. Manually trigger the `release-pypi.yaml` in `dry-run` mode to build cross-compiled binaries. Check `dry-run` output lists and ensure all desired wheels are built.
3. Manually trigger the `release-pypi.yaml` in publish mode.
4. Confirm successful PyPI upload.
5. Tag the release with `git tag -a {prefix-version} -m "Release version #.#.#"`.
    a. For example, the `imgal_python` release tag looks like `git tag -a imgal_python-v0.1.0 -m "Release version 0.1.0"`.
6. Next push the tag to GitHub with `git push origin {prefix-version}`.
    a. For example, the `imgal_python` release tag push looks like `git push origin imgal_python-v0.1.0`.
7. Bump the minor version number in the `Cargo.toml` and the `pyproject.toml`.
