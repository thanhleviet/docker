#https://github.com/HPCBio/16S-rDNA-dada2-pipeline
FROM bioconductor/release_core2

LABEL project="dada2"
LABEL version="release"

MAINTAINER Katie Lennard

RUN R -e 'source("https://bioconductor.org/biocLite.R"); biocLite("dada2"); biocLite("DECIPHER"); biocLite("biomformat")'
RUN R -e 'install.packages(c("phangorn","dplyr"), dependencies=TRUE)'

#CMD ["R"]

CMD ["/bin/bash"]

################## Hex specific ###########################
#RUN mkdir -p /researchdata/fhgfs
