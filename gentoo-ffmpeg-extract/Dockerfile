FROM gentoo/portage as portage
FROM gentoo/stage3-amd64 as builder
COPY --from=portage /usr/portage /usr/portage

RUN echo GENTOO_MIRRORS="http://ftp.iij.ad.jp/pub/linux/gentoo/" >> /etc/portage/make.conf
RUN echo 'CPU_FLAGS_X86="aes avx avx2 fma3 mmx mmxext pclmul popcnt sse sse2 sse3 sse4_1 sse4_2 ssse3"' >> /etc/portage/make.conf

RUN echo 'media-video/ffmpeg -fftools_cws2fws -zlib -bzip2 -iconv -network cpudetection gpl libsoxr postproc x264' > /etc/portage/package.use/ffmpeg \
 && mkdir -p /etc/portage/package.accept_keywords && echo '=media-video/ffmpeg-3.4 ~amd64' > /etc/portage/package.accept_keywords/ffmpeg
RUN emerge 'media-video/ffmpeg'

RUN ffmpeg -version
RUN ffprobe -version

COPY extract /
RUN /extract /rootfs /usr/bin/ffmpeg
RUN /extract /rootfs /usr/bin/ffprobe

FROM scratch
COPY --from=builder /rootfs /
