FROM continuumio/miniconda3:4.2.2

LABEL maintainer="Thanh Le Viet"
LABEL description="mamba for conda"
LABEL maintainer.email="lethanhx2k@gmail.com"

RUN apt-get update \
    && apt-get clean -y \
    && conda install -c conda-forge mamba=0.6.3\
    && conda clean -a -y

ENV PATH /opt/conda/bin/:$PATH