VERSION --pass-args 0.7
PROJECT earthly-technologies/earthfile-grammar

FROM node:20.10.0-alpine3.18
RUN npm install -g @vscode/vsce ovsx semver
WORKDIR /earthfile-syntax-highlighting

# package builds the Earthfile Syntax Highlighting package locally as a vscode extension
package:
    COPY . ./
    ARG --required VSCODE_RELEASE_TAG
    RUN VERSION=${VSCODE_RELEASE_TAG#v} ; \
        sed -i 's^0.0.0^'"$VERSION"'^g' ./package.json
    RUN vsce package
    RUN VERSION=${VSCODE_RELEASE_TAG#v} ; \
        mv ./earthfile-syntax-highlighting-$VERSION.vsix ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix
    SAVE ARTIFACT ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix

# local creates a new package in the local filesystem
local:
    ARG --required VSCODE_RELEASE_TAG
    FROM --pass-args +package
    SAVE ARTIFACT ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix AS LOCAL ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix

# local-install produces an extension in the local filesystem and installs it with code cli
local-install:
    LOCALLY
    ARG --required VSCODE_RELEASE_TAG
    WAIT
        BUILD --pass-args +local
    END
    RUN code --install-extension earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix

# release publishes the Earthfile Syntax Highlighting package as a vscode extension
# directly to the VS Code Marketplace and Open Vsx
release:
    ARG --required VSCODE_RELEASE_TAG
    COPY --pass-args +package/earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix ./
    RUN --secret VSCE_TOKEN=vsce-token test -n "$VSCE_TOKEN"
    RUN --secret OVSX_TOKEN=ovsx-token test -n "$OVSX_TOKEN"
    RUN --push \
        --secret VSCE_TOKEN=vsce-token \
        vsce publish --pat "$VSCE_TOKEN" --packagePath ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix
    RUN --push \
        --secret OVSX_TOKEN=ovsx-token \ 
        npx ovsx publish ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix -p "$OVSX_TOKEN"

export:
    COPY . ./
    SAVE ARTIFACT ./
