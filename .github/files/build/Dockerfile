# syntax=docker/dockerfile:1.8.0@sha256:d6d396f3780b1dd56a3acbc975f57bd2fc501989b50164c41387c42d04e780d0
FROM --platform=$BUILDPLATFORM busybox:1.36.1-uclibc@sha256:97d85ff9630b634ddff3e3ff69fd02bc3b69de8dba0c5002eb0ad6915d1bf4c0 AS env
ARG TARGETPLATFORM
RUN --mount=type=bind,source=artifact,target=artifact \
    if [ "$TARGETPLATFORM" = 'linux/amd64' ]; then\
      cp artifact/x86_64-unknown-linux-musl/cpuusage .\
    ;elif [ "$TARGETPLATFORM" = 'linux/arm64' ]; then\
      cp artifact/aarch64-unknown-linux-musl/cpuusage .\
    ;fi

FROM --platform=$BUILDPLATFORM scratch as runner
COPY --from=env --chmod=755 cpuusage .
ENTRYPOINT ["./cpuusage"]
