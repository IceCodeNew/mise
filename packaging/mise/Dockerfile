# syntax=docker/dockerfile:1@sha256:b6afd42430b15f2d2a4c5a02b919e98a525b785b1aaff16747d2f623364e39b6
FROM rust@sha256:0e18a916cc41ed3a99356ded9b3c8b0f91e15249d4507a18ec9af4edb7a631e5 AS builder
LABEL maintainer="jdx"
LABEL org.opencontainers.image.source=https://github.com/jdx/mise
LABEL org.opencontainers.image.description="mise is a tool for managing your development environment"
LABEL org.opencontainers.image.licenses=MIT

WORKDIR /usr/src/mise
COPY . /usr/src/mise/
RUN cargo build --release

FROM rust@sha256:0e18a916cc41ed3a99356ded9b3c8b0f91e15249d4507a18ec9af4edb7a631e5 AS runtime

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ENV MISE_DATA_DIR="/mise"
ENV MISE_CONFIG_DIR="/mise"
ENV MISE_CACHE_DIR="/mise/cache"
ENV PATH="/mise/shims:$PATH"
ENV MISE_CACHE_PRUNE_AGE="10y"

COPY --from=builder /usr/src/mise/target/release/mise /usr/local/bin/mise

RUN <<EOT
set -euxo pipefail

apt-get update && apt-get install -y \
    jq                               \
    python3-full                     \
    python3-pip
rm -rf /var/lib/apt/lists/* && apt-get clean

mise use -g python@latest

mise -v
EOT

WORKDIR /mise
ENTRYPOINT ["mise"]
CMD ["--help"]
