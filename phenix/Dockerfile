# Base Image
FROM biocontainers/biocontainers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="1"
LABEL software="PHEnix"
LABEL software.version="1.3 commit bcbba63"
LABEL description="Public Health England SNP calling Pipeline"
LABEL website="https://github.com/phe-bioinformatics/PHEnix"
LABEL documentation="http://phenix.readthedocs.io/en/latest/"
LABEL license="https://github.com/phe-bioinformatics/PHEnix/blob/master/LICENSE"
LABEL tags="General,Genomics,SNP"

# Maintainer
MAINTAINER Le Viet Thanh <thanhlv@oucru.org>

COPY tools/GenomeAnalysisTK-3.7-0.tar.bz2 /home/biodocker/bin

RUN conda install bwa \
                  samtools \
                  bcftools \
                  bwa \
                  bowtie2 \
                  picard \
                  gatk=3.7

RUN gatk-register /home/biodocker/bin/GenomeAnalysisTK-3.7-0.tar.bz2


RUN pip install --no-cache-dir numpy \
                               biopython\
                               bintrees \
                               matplotlib \
                               argparse \
                               PyYAML\
                               PyVCF &&\
    git clone https://github.com/phe-bioinformatics/PHEnix.git /home/biodocker/bin/PHEnix &&\
    mv /home/biodocker/bin/PHEnix/phe /home/biodocker/bin/PHEnix/scripts/phe &&\
    sed -i '1i\#!/usr/bin/env python' /home/biodocker/bin/PHEnix/scripts/prepare_reference.py &&\
    sed -i '1i\#!/usr/bin/env python' /home/biodocker/bin/PHEnix/scripts/filter_vcf.py &&\
    sed -i '1i\#!/usr/bin/env python' /home/biodocker/bin/PHEnix/scripts/vcf2fasta.py
    # chmod +x /home/biodocker/bin/PHEnix/scripts/*.py

ENV PATH=${PATH}:/home/biodocker/bin/PHEnix/scripts
ENV GATK_JAR=/opt/conda/opt/gatk-3.7/GenomeAnalysisTK.jar
ENV PICARD_JAR=/opt/conda/share/picard-2.9.2-1/picard.jar

RUN conda clean -a

WORKDIR /data/
