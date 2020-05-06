# build stage
FROM alpine:3.11.6 as builder

ARG UPX_VERSION=3.96

RUN echo https://mirrors.aliyun.com/alpine/v3.11/main > /etc/apk/repositories \
	&& echo https://mirrors.aliyun.com/alpine/v3.11/community >> /etc/apk/repositories

# download source and compile
RUN apk add --no-cache \
    build-base \
    wget \
    xz \
    && wget https://github.com/upx/upx/releases/download/v${UPX_VERSION}/upx-${UPX_VERSION}-amd64_linux.tar.xz \
    && xz -d -c /upx-${UPX_VERSION}-amd64_linux.tar.xz | tar -xOf - upx-${UPX_VERSION}-amd64_linux/upx > /bin/upx \
    && chmod a+x /bin/upx

# final stage
FROM alpine:3.11.6

COPY --from=builder /bin/upx /bin/upx

ENTRYPOINT ["/bin/upx"]