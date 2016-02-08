FROM ubuntu:trusty
MAINTAINER John Ramey <johnramey@gmail.com>

# Instructions mostly from:
# https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu
# More details available from:
# https://gist.github.com/xdamman/e4f713c8cd1a389a5917

# Add multiverse for AAC codec (libfaac-dev)
RUN echo 'deb http://archive.ubuntu.com/ubuntu trusty universe multiverse' >> /etc/apt/sources.list

# Dependencies
RUN apt-get update -y && apt-get install -y \
    autoconf \
    automake \
    build-essential \
    ca-certificates \
    libass-dev \
    libfaac-dev \
    libfreetype6-dev \
    libopencore-amrnb-dev \
    libopencore-amrwb-dev \
    librtmp-dev \
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
    wget \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# Other codecs unavailable for install via apt-get
ENV TMP_PATH /tmp/ffmpeg_sources
RUN mkdir -p $TMP_PATH

# H.265/HEVC video codec
WORKDIR $TMP_PATH
RUN hg clone https://bitbucket.org/multicoreware/x265 \
    && cd $TMP_PATH/x265/build/linux \
    && cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="/usr/local" -DENABLE_SHARED:bool=off ../../source \
    && make \
    && make install

# VP8/VP9 video codec
WORKDIR $TMP_PATH
RUN git clone https://chromium.googlesource.com/webm/libvpx \
    && cd libvpx \
    && ./configure --disable-examples --disable-unit-tests --prefix=/usr/local \
    && make \
    && make install

# Install ffmpeg
WORKDIR $TMP_PATH
RUN git clone --depth 1 git://source.ffmpeg.org/ffmpeg \
    && cd ffmpeg \
    && ./configure --prefix=/usr/local --pkg-config-flags="--static" \
    --extra-cflags="-I$/usr/local/include" --extra-ldflags="-L/usr/local/lib" \
    --enable-gpl --enable-libmp3lame --enable-libopencore-amrnb \
    --enable-libopencore-amrwb --enable-librtmp --enable-libtheora --enable-libvorbis \
    --enable-libvpx --enable-libx264 --enable-nonfree --enable-version3 \
    # --enable-libfaac
    && make \
    && make install \
    && make distclean

RUN rm -rf $TMP_PATH

#ENTRYPOINT [ "ffmpeg-docker" ]