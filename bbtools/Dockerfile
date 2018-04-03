FROM openjdk:alpine

MAINTAINER Thanh Le Viet <lethanhx2k@gmail.com>


RUN apk add --update --no-cache bash wget \
    && rm -rf /var/cache/apk/*

ENV BBTOOLS_SOURCE="BBMap_37.87.tar.gz" \
    BBTOOLS_HOME="/opt/bbtools"

RUN mkdir -p $BBTOOLS_HOME \
    && cd $BBTOOLS_HOME \
    && wget "https://ncu.dl.sourceforge.net/project/bbmap/$BBTOOLS_SOURCE" \
    && tar -xvzf $BBTOOLS_SOURCE \
    && mv bbmap/* . \
    && rm $BBTOOLS_SOURCE \
    && rm -r bbmap

ENV PATH $BBTOOLS_HOME:$PATH

RUN apk del wget

CMD ["/bin/bash"]
