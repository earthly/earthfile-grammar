VERSION 0.7
FROM node:19.1.0-alpine3.15
RUN npm install -g vsce ovsx semver
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

local:
    ARG --required VSCODE_RELEASE_TAG
    FROM --build-arg VSCODE_RELEASE_TAG="$VSCODE_RELEASE_TAG" +package
    SAVE ARTIFACT ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix AS LOCAL ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix

# release publishes the Earthfile Syntax Highlighting package as a vscode extension
# directly to the VS Code Marketplace and Open Vsx
release:
    ARG --required VSCODE_RELEASE_TAG
    COPY --build-arg VSCODE_RELEASE_TAG="$VSCODE_RELEASE_TAG" +package/earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix ./
    RUN --secret VSCE_TOKEN=+secrets/earthly-technologies/vsce/token test -n "$VSCE_TOKEN"
    RUN --secret OVSX_TOKEN=+secrets/earthly-technologies/ovsx/token test -n "$OVSX_TOKEN"
    RUN --push \
        --secret VSCE_TOKEN=+secrets/earthly-technologies/vsce/token \
        vsce publish --pat "$VSCE_TOKEN" --packagePath ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix
    RUN --push \
        --secret OVSX_TOKEN=+secrets/earthly-technologies/ovsx/token \ 
        npx ovsx publish ./earthfile-syntax-highlighting-$VSCODE_RELEASE_TAG.vsix -p "$OVSX_TOKEN"

export:
    COPY . ./
    SAVE ARTIFACT ./