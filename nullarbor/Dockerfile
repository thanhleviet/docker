FROM continuumio/miniconda3

MAINTAINER Thanh Le Viet lethanhx2k@gmail.com

# RUN apt-get update &&\
    # apt-get install -y build-essential &&\
    # cpan YAML::Tiny 
    # cpanm YAML::Tiny

RUN conda install -c bioconda perl-yaml-tiny \
                              perl-path-tiny \
                              perl-moo \
                              perl-bioperl \
                              perl-text-csv

RUN conda install -c bioconda -c conda-forge seqtk \
                              trimmomatic \
                              shovill \
                              snippy \
                              prokka \
                              quicktree \
                              iqtree \
                              roary \
                              mlst \
                              abricate \
                              snp-dists \
                              trimmomatic \
                              kraken\
                              kraken2\
                              mash=2.1 \
                              centrifuge \
                              newick_utils

RUN git clone https://github.com/tseemann/nullarbor.git

ENV PATH="/nullarbor/bin:${PATH}"
ENV KRAKEN_DEFAULT_DB=/database/minikraken_20171019_4GB
ENV CENTRIFUGE_DEFAULT_DB=/database/centrifuge-db/p_compressed+h+v

#RUN nullarbor.pl --check

CMD [ "/bin/bash" ]
#CMD [ "nullarbor.pl" ]
