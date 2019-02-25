FROM nfcore/base
LABEL description="campy"
COPY environment.yml /
RUN conda update -n base -c defaults conda \
    && conda env create -f /environment.yml && conda clean -a
ENV PATH /opt/conda/envs/campy/bin:$PATH
