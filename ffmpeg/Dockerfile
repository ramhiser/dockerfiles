FROM ubuntu:trusty
MAINTAINER John Ramey <johnramey@gmail.com>

# Instructions mostly from:
# https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu
# More details available from:
# https://gist.github.com/xdamman/e4f713c8cd1a389a5917

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN apt-add-repository ppa:mc3man/trusty-media
RUN apt-get update
RUN apt-get install -y ffmpeg

ENTRYPOINT [ "ffmpeg" ]
