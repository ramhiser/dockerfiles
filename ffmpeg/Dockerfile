FROM ubuntu:trusty
MAINTAINER John Ramey <johnramey@gmail.com>

# Simple ffmpeg build from:
# http://fcorti.com/2014/04/22/ffmpeg-ubuntu-14-04-lts/
# Other ffmpeg instructions from:
# https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN apt-add-repository ppa:mc3man/trusty-media
RUN apt-get update
RUN apt-get install -y ffmpeg

ENTRYPOINT [ "ffmpeg" ]
