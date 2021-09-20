# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.177.0/containers/debian/.devcontainer/base.Dockerfile

# [Choice] Debian version: bullseye, buster, stretch
ARG VARIANT=buster
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# ** [Optional] Uncomment this section to install additional packages. **
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

COPY install-tl.profile.txt /tmp/
# hadolint ignore=DL3008
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        chktex \
        libfile-homedir-perl \
        libunicode-linebreak-perl \
        libyaml-tiny-perl \
    ; \
    curl -sSL -o /tmp/install-tl.tar.gz https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz; \
    mkdir /tmp/install-tl; \
    tar -x -f /tmp/install-tl.tar.gz -C /tmp/install-tl --strip-components=1; \
    /tmp/install-tl/install-tl -no-gui -profile /tmp/install-tl.profile.txt; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*; \
    rm -rf /tmp/install-tl*;
ENV PATH="${PATH}:/usr/local/texlive/2021/bin/x86_64-linux"
RUN set -eux; \
    tlmgr install \
        academicons \
        arydshln \
        babel-french \
        datenumber \
        fontawesome5 \
        fontaxes \
        fontspec \
        hyphen-french \
        latexindent \
        latexmk \
        lualatex-math \
        luatexbase \
        moderncv \
        multirow \
        opensans \
        pgf \
        unicode-math \
        xkeyval \
    ; \
    chown -R vscode:vscode /usr/local/texlive;
