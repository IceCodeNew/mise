FROM fedora:44@sha256:8a396124f358d2922f1b1c40aee2e7f1dd016b26b3d525d4338e7da12c1cd9a5
LABEL maintainer="jdx"

# Install packaging dependencies
RUN dnf update -y && \
    dnf install -y \
        rpm-build \
        rpmdevtools \
        python3-pip \
        git \
        rust \
        cargo \
        gcc \
        tar \
        gzip && \
    dnf clean all

# Install copr-cli
RUN pip3 install copr-cli

# Add mise to PATH
ENV PATH="/root/.local/bin:${PATH}"

# Install mise and use it to install cargo-vendor
RUN curl https://mise.run | sh
RUN mise use -g cargo-binstall cargo:cargo-vendor

# Set up RPM build environment
RUN rpmdev-setuptree
