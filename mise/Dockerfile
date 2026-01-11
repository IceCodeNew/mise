# syntax=docker/dockerfile:1

FROM mirror.gcr.io/library/alpine:3.23 AS bin-check
ARG CACHE_BUST
COPY --link --from=bin_mise ./mise /emptydir/
RUN /emptydir/mise --version


FROM mirror.gcr.io/library/alpine:3.23 AS final
LABEL maintainer="IceCodeNew"
RUN <<EOT
set -euxo pipefail

apk update
apk --no-progress --no-cache add \
    ca-certificates curl \
    bash catatonit tzdata
rm -rf /var/cache/apk/*
sed -i 's!/bin/ash!/bin/bash!' /etc/passwd
EOT
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV MISE_DATA_DIR="/mise" \
    MISE_CONFIG_DIR="/mise" \
    MISE_CACHE_DIR="/mise/cache" \
    MISE_CACHE_PRUNE_AGE="10y" \
    PATH="/mise/shims:$PATH"
WORKDIR /mise/
COPY --link --from=bin-check /emptydir/ /usr/local/bin/

ENTRYPOINT [ "catatonit", "--", "mise" ]
CMD [ "--help" ]
