#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See https://go.microsoft.com/fwlink/?linkid=2090316 for license information.
#-------------------------------------------------------------------------------------------------------------

# To fully customize the contents of this image, use the following Dockerfile instead:
# https://github.com/microsoft/vscode-dev-containers/tree/v0.112.0/containers/javascript-node-12/.devcontainer/Dockerfile
FROM ocaml/opam2

# The image referenced above includes a non-root user with sudo access. Add
# the "remoteUser" property to devcontainer.json to use it. On Linux, the container
# user's GID/UIDs will be updated to match your local UID/GID when using the image
# or dockerFile property. Update USER_UID/USER_GID below if you are using the
# dockerComposeFile property or want the image itself to start with different ID
# values. See https://aka.ms/vscode-remote/containers/non-root-user for details.
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG USERNAME=opam 

# [Optional] Update UID/GID if needed
RUN if [ "$USER_GID" != "1000" ] || [ "$USER_UID" != "1000" ]; then \
        groupmod --gid $USER_GID $USERNAME \
        && usermod --uid $USER_UID --gid $USER_GID $USERNAME \
        && chown -R $USER_UID:$USER_GID /home/$USERNAME; \
    fi

#
ENV DEBIAN_FRONTEND=noninteractive

RUN sudo apt-get update \
    && sudo apt-get -y install m4 \
    #
    # Clean up
    && sudo apt-get autoremove -y \
    && sudo apt-get clean -y \
    && sudo rm -rf /var/lib/apt/lists/*


RUN opam update -y \
    && opam depext merlin \
    && opam depext ocp-indent \
    && opam depext ocamlformat \
    && opam install -y merlin \
    && opam install -y ocp-indent \
    && opam install -y ocamlformat

USER ${USERNAME}
RUN opam init -a

ENV DEBIAN_FRONTEND=dialog
