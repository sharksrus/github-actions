FROM public.ecr.aws/docker/library/alpine:3.18.2
LABEL maintainer="Glen Stummer <glen@glen.dev>"

ENV TFSEC_VERSION=1.28.1

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]
COPY entrypoint.sh /entrypoint.sh

# hadolint ignore=DL3018
RUN addgroup -S shark -g 1000 && adduser -S shark -u 1000 -G shark &&\
    apk add --no-cache --virtual .build-deps \
    zip \
    wget &&\
    wget --progress=dot:giga https://github.com/tfsec/tfsec/releases/download/v${TFSEC_VERSION}/tfsec-linux-amd64 &&\
    chmod +x  tfsec-linux-amd64 &&\
    mv tfsec-linux-amd64 /usr/local/bin/tfsec &&\
    chown shark:shark /usr/local/bin/tfsec &&\
    chmod +x /entrypoint.sh &&\
    chown shark:shark /entrypoint.sh &&\
    apk del --purge .build-deps

USER shark
ENTRYPOINT ["/entrypoint.sh"]
