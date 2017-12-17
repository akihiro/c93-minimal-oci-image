FROM ubuntu
RUN apt-get update \
 && apt-get install -y --no-install-recommends ffmpeg \
 && rm -rf /var/lib/apt/lists/*
COPY extract /
RUN /extract /rootfs /usr/bin/ffmpeg
RUN /extract /rootfs /usr/bin/ffprobe
RUN ls -laR /rootfs

FROM scratch
COPY --from=0 /rootfs /
