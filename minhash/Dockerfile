FROM quay.io/biocontainers/seqtk:1.2--1

MAINTAINER Thanh Le Viet <lethanhx2k@gmail.com>

RUN opkg-install curl ca-bundle zlib

RUN curl -LJO https://github.com/marbl/Mash/releases/download/v2.0/mash-Linux64-v2.0.tar &&\
    tar xvf mash-Linux64-v2.0.tar &&\
    mv mash-Linux64-v2.0/mash bin/mash &&\
    rm -r mash-Linux64-v2.0 &&\
    rm mash-Linux64-v2.0.tar

RUN curl -LJO https://github.com/onecodex/finch-rs/releases/download/v0.1.5/finch-linux64-v0.1.5.tar.gz &&\
    gunzip finch-linux64-v0.1.5.tar.gz &&\
    tar xvf finch-linux64-v0.1.5.tar &&\
    mv finch-linux64-v0.1.5/finch bin/finch &&\
    rm -r finch-linux64-v0.1.5 &&\
    rm finch-linux64-v0.1.5.tar

CMD ["/bin/bash"]
