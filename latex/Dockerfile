FROM gliderlabs/alpine:3.3

echo '@testing http://nl.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories

# TODO: Currently, poppler installs libpoppler.so.57 in /usr/lib
# However, texlive requires libpoppler.so.58. I'm going to wait a short time to
# see if the versions catch up with each other instead of burning a lot of time
# on this.
RUN apk update \
    poppler \
    texlive \
    && rm -rf /var/cache/apk/*
