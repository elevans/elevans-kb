crates.io release
===

## Publishing a crate on crates.io

### Update the version number and create a Git tag

1. Bump the version number of the crate and create a commit with `Release {name} version #.#.#`.
    a. Pro-tip: You can make an empty commit like this: `git commit --allow-empty -m "Release {name} version #.#.#`.
2. Tag the release with `git tag -a {prefix-version} -m "Release version #.#.#"`.
   For example, the `imgal` core Rust library release looks like `git tag -a imgal-v0.1.0 -m "Release {name} version 0.1.0"`.
3. Push the tag to GitHub with `git push origin {prefix-version}`. For example, the `imgal` release tag push looks like `git push origin imgal-v0.1.0`.
4. Bump the minor version number in the `Cargo.toml` and commit "Bump {name} to the next development cycle".

### Publish the crate on crates.io

*Note: Do not publish crates from the workspace, instead specify the crate to publish with the `-p` flag.*

1. Login with your crates.io API token.
2. Checkout tagged release version.
3. Perform a dry run before publishing to ensure no build erros or packing errors occur. 

    ```bash
    $ cargo publish -p imgal --dry-run
    ```

4. Check the contents of the crate to ensure that unnecessary/unintended resources are not included:

    ```bash
    $ cargo package --list -p imgal
    ```
5. Publish the crate with:

    ```bash
    $ crago publish -p imgal
    ```
