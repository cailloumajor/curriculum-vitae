# [Choice] Debian version (use bullseye on local arm64/Apple Silicon): bookworm, bullseye, buster
ARG VARIANT="bookworm"
FROM buildpack-deps:${VARIANT}-curl

# [Optional] Uncomment this section to install additional OS packages.
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
