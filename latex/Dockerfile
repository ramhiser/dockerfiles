FROM gliderlabs/alpine:3.3

echo '@testing http://nl.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories

# TODO: Currently, poppler installs libpoppler.so.57 in /usr/lib
# However, texlive requires libpoppler.so.58. I'm going to wait a short time to
# see if the versions catch up with each other instead of burning a lot of time
# on this.
RUN apk update \
    poppler \

# HACK
# Source: http://jhshi.me/2011/11/10/pdflatex-error-while-loading-shared-libraries-libpoppler-so-13/
RUN ln -s /usr/lib/libpoppler.so.57 /usr/lib/libpoppler.so.58

RUN apk add texlive@testing
    texlive@testing \
    && rm -rf /var/cache/apk/*
