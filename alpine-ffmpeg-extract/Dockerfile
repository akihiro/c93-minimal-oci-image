FROM alpine
RUN apk add --no-cache ffmpeg
RUN apk add --no-cache bash coreutils
COPY extract /
RUN /extract /rootfs /usr/bin/ffmpeg
RUN /extract /rootfs /usr/bin/ffprobe

FROM scratch
COPY --from=0 /rootfs /
