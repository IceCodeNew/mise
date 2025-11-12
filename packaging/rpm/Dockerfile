FROM fedora:44@sha256:8a396124f358d2922f1b1c40aee2e7f1dd016b26b3d525d4338e7da12c1cd9a5
LABEL maintainer="jdx"

RUN dnf install -y rpm-build rpm-sign ruby ruby-devel gcc \
      && gem install fpm \
      && dnf install -y createrepo \
      && dnf clean all
