FROM ubuntu:16.04

# MAINTAINER Tim Massingham <tim.massingham@nanoporetech.com>
MAINTAINER Thanh Le Viet <lethanhx2k@gmail.com>

RUN apt-get update && apt-get install -y --no-install-recommends  \
    ca-certificates git libopenblas-dev libhdf5-dev cmake make libcunit1-dev

RUN git clone --depth 1 https://github.com/nanoporetech/scrappie.git

RUN cd scrappie && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make && \
    make test &&\
    make install

# ENV PATH=$PATH:/scrappie

RUN groupadd fuse \
    && useradd --create-home --shell /bin/bash --user-group --uid 1000 --groups sudo,fuse biodocker && \
    echo `echo "biodocker\nbiodocker\n" | passwd biodocker`\
    && apt-get remove -y git wget cmake\
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

# Change user
USER biodocker

CMD ["/bin/bash"]
