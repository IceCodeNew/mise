FROM ubuntu:24.04@sha256:e96e81f410a9f9cae717e6cdd88cc2a499700ff0bb5061876ad24377fcc517d7
LABEL maintainer="jdx"

RUN apt-get update \
    && apt-get install -y \
        build-essential \
        ruby \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN gem install fpm
