# earthfile-syntax-highlighting

<div align="center"><img alt="Earthly" width="700px" src="https://github.com/earthly/earthly/raw/main/img/logo-banner-white-bg.png" /></div>

Syntax highlighting for [Earthly](https://earthly.dev) Earthfiles.

For an introduction of Earthly see the [Earthly GitHub repository](https://github.com/earthly/earthly) or the [Earthly documentation](https://docs.earthly.dev).

## How to Test

```
# Build & Install the package
earthly +local-install --VSCODE_RELEASE_TAG=${VERSION}
```

## How to Release

1. Check what the next version should be by looking [what is already published]((https://marketplace.visualstudio.com/items?itemName=earthly.earthfile-syntax-highlighting))
2. Set the version to publish:
    ```bash
    export VSCODE_RELEASE_TAG=${NEW_VERSION_HERE}
    ```
3. Make sure that the new version has release notes already in the [README](https://github.com/earthly/earthfile-grammar/CHANGELOG.md)
4. Run:
    ```bash
    earthly --release --VSCODE_RELEASE_TAG=${VSCODE_RELEASE_TAG}
    ```
5. Finally, tag git for future reference
    ```bash
    git tag "vscode-syntax-highlighting-$VSCODE_RELEASE_TAG"
    git push origin "vscode-syntax-highlighting-$VSCODE_RELEASE_TAG"
    ```

### troubleshooting

- If `VSCE_TOKEN` token has expired, Vlad can regenerate one following [this guide](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#get-a-personal-access-token) and then setting it using `earthly secrets --org earthly-technologies --project earthfile-grammar set vsce-token '...'`. Vlad - use your GitHub / gmail Microsoft account.

- If `OVSX_TOKEN` token has expired, Nacho can regenerate one following [this guide](https://github.com/eclipse/openvsx/wiki/Publishing-Extensions#3-create-an-access-token) and then setting it using `earthly secrets --org earthly-technologies --project earthfile-grammar set ovsx-token '...'`


## Release Notes

[Changelog](./CHANGELOG.md)
