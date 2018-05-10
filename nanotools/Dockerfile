FROM ubuntu:16.04

# base software
RUN apt-get update &&\
    apt-get install -y --no-install-recommends\
    git \
    cmake \
    build-essential \
    software-properties-common \
    wget \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libncurses5-dev \
    autoconf \
    python-setuptools \
    libhts-dev

#Java
ENV DEBIAN_FRONTEND noninteractive
ENV JAVA_HOME       /usr/lib/jvm/java-8-oracle
ENV LANG            en_US.UTF-8
ENV LC_ALL          en_US.UTF-8

RUN apt-get install -y --no-install-recommends locales && \
    locale-gen en_US.UTF-8 && \
    apt-get --purge remove openjdk* && \
    echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > /etc/apt/sources.list.d/webupd8team-java-trusty.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
    apt-get update && \
    apt-get install -y --no-install-recommends oracle-java8-installer oracle-java8-set-default

# python and python dependencies
RUN apt-get install -y --no-install-recommends python python-pip \
    && pip install pysam pyvcf biopython clint \
    && add-apt-repository ppa:jonathonf/python-3.6 \
    && apt-get update \
    && apt-get install -y --no-install-recommends python3.6 python3-setuptools


ENV nanopolish_version=v0.8.4
ENV bwa_version=v0.7.17
ENV samtools_version=1.5

#Nanopolish
RUN git clone --recursive https://github.com/jts/nanopolish/ \
    && cd nanopolish \
    && git checkout tags/$nanopolish_version \
    && make -j4

#BWA
RUN git clone https://github.com/lh3/bwa \
    && cd bwa \
    && git checkout tags/$bwa_version \
    && make

#Samtools
RUN wget https://github.com/samtools/samtools/releases/download/$samtools_version/samtools-$samtools_version.tar.bz2 \
    && tar xjf samtools-$samtools_version.tar.bz2 \
    && cd samtools-$samtools_version \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    && mv samtools-$samtools_version samtools \
    && rm samtools-$samtools_version.tar.bz2

#Racon
RUN git clone --recursive https://github.com/isovic/racon.git racon \
    && cd racon \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_BUILD_TYPE=Release .. \
    && make \
    && make install

#Minimap2
RUN git clone https://github.com/lh3/minimap2 \
    && cd minimap2 \
    && make

#Miniasm
RUN git clone https://github.com/lh3/miniasm \
    && cd miniasm \
    && make

#Unicycler
RUN git clone https://github.com/rrwick/Unicycler.git \
    && cd Unicycler \
    && python3 setup.py install

#Porechop
RUN git clone https://github.com/rrwick/Porechop.git \
    && cd Porechop \
    && python3 setup.py install

#Canu
RUN git clone https://github.com/marbl/canu.git \
    && cd canu/src \
    && git checkout c9ef9219 \
    && make -j 8 \
    && cd / \
    && chmod -R 775 canu
#Blast

RUN wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.6.0/ncbi-blast-2.6.0+-x64-linux.tar.gz && \
    tar xzf ncbi-blast-2.6.0+-x64-linux.tar.gz

#Fix nanopolish script executable
RUN sed -i '1i #!/usr/bin/env python' /nanopolish/scripts/nanopolish_makerange.py \
    && chmod +x /nanopolish/scripts/nanopolish_makerange.py \
    && sed -i '1i #!/usr/bin/env python' /nanopolish/scripts/nanopolish_merge.py \
    && chmod +x /nanopolish/scripts/nanopolish_merge.py


ENV PATH $PATH:/nanopolish:/nanopolish/scripts:/bwa:/samtools:/minimap2:/miniasm:/canu/Linux-amd64/bin:/ncbi-blast-2.6.0+/bin

# Add user biodocker with password biodocker
# https://github.com/BioContainers/containers/blob/master/biodocker/Dockerfile
RUN groupadd fuse \
    && useradd --create-home --shell /bin/bash --user-group --uid 1000 --groups sudo,fuse biodocker && \
    echo `echo "biodocker\nbiodocker\n" | passwd biodocker`\
    && rm -rf /var/lib/apt/lists/*

# Change user
USER biodocker

CMD ["/bin/bash"]
