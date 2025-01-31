PyPi release
===

## Remove project `dev` version and create a Git tag

1. Confirm the repository CI jobs are passing.
2. Remove the `dev0` label from the project version in the `pyproject.toml` or `setup.py` file.
3. Create a new commit with `Release version #.#.#`.
4. Tag the commit with `git tag #.#.#` where `#.#.#` is the version number.
5. Bump the project minor version number, add back the `dev0` to the version number and commit with "Bump to next development cycle".
6. Push the commits and push the tag. To push the tag use the following command: `git push origin 1.10.0`. With out this command tags are stored only locally.

## Publish the package on PyPi

1. Checkout the appropriate version tag.
    - For example: `git checkout 1.10.0`
2. Build the Python package with `python -m build` (_Note_: You can install `build` from PyPi with `pip install build`).
3. Upload to PyPi with `twine upload dist/*`
