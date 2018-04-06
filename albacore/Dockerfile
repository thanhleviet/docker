FROM ubuntu:16.04
MAINTAINER Thanh Le Viet lethanhx2k@gmail.com


RUN apt-get update && \
 apt-get upgrade -y && \
 apt-get install -y wget apt-transport-https libboost-all-dev python3-setuptools

#Update: 02/04/2018
ENV DEB_URL https://mirror.oxfordnanoportal.com/software/analysis/python3-ont-albacore_2.2.6-1~xenial_amd64.deb

RUN wget -O- https://mirror.oxfordnanoportal.com/apt/ont-repo.pub | apt-key add - &&\
    echo "deb http://mirror.oxfordnanoportal.com/apt trusty-stable non-free" | tee /etc/apt/sources.list.d/nanoporetech.sources.list &&\
    apt-get update &&\
    wget -qO albacore.deb $DEB_URL &&\
    dpkg -i albacore.deb || : &&\
    apt-get install -fy

ENTRYPOINT ["read_fast5_basecaller.py"]

CMD ["-h"]
