FROM ubuntu:trusty
MAINTAINER John Ramey <johnramey@gmail.com>
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Instructions mostly from:
# https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu
# More details available from:
# https://gist.github.com/xdamman/e4f713c8cd1a389a5917

# Dependencies
RUN apt-get update -y && apt-get install -y \
    autoconf \
    automake \
    build-essential \
    ca-certificates \
    cmake-curses-gui \
    libass-dev \
    libfreetype6-dev \
    libsdl1.2-dev \
    libtheora-dev \
    libtool \
    libva-dev \
    libvdpau-dev \
    libvorbis-dev \
    libxcb1-dev \
    libxcb-shm0-dev \
    libxcb-xfixes0-dev \
    pkg-config \
    texinfo \
    zlib1g-dev \
    yasm \
    libx264-dev \
    libmp3lame-dev \
    libopus-dev \
    git \
    cmake \
    mercurial \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# Other Encoders/Decoders unavailable for install via apt-get
ENV TMP_PATH /tmp/ffmpeg_sources
RUN mkdir -p $TMP_PATH

# H.265/HEVC video encoder

WORKDIR $TMP_PATH
RUN hg clone https://bitbucket.org/multicoreware/x265 \
    && cd $TMP_PATH/x265/build/linux \
    && ./make-Makefiles.bash

WORKDIR $TMP_PATH/x265/build/linux
RUN echo ${TMP_PATH}/make-Makefiles.bash
RUN /bin/bash -c "source ${TMP_PATH}/x265/build/linux/make-Makefiles.bash"
RUN make \
    && make install \
    && make distclean

# AAC audio encoder
# TODO

# VP8/VP9 video encoder and decoder
# TODO

# Install ffmpeg
WORKDIR $TMP_PATH
RUN git clone --depth 1 git://source.ffmpeg.org/ffmpeg
WORKDIR $TMP_PATH/ffmpeg
#RUN ./configure --enable-gpl --enable-libfaac --enable-libmp3lame
#    --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-librtmp \
#    --enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 \
#    --enable-nonfree --enable-version3
#RUN make

#RUN cd FFmpeg && ./configure && make && make install

# RUN rm -rf /tmp/ffmpeg_sources

#ENTRYPOINT [ "ffmpeg-docker" ]