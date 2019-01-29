FROM centos:centos7

LABEL maintainer="lethanhx2k@gmail.com"


COPY install_aspera_connect.sh /tmp/install.sh

# Shamelessly stolen from https://github.com/aertslab/install_aspera_connect
RUN aspera_connect_url=$(curl 'https://downloads.asperasoft.com/en/downloads/8?list' \
      | grep -oE 'https://download.asperasoft.com/download/sw/connect/[0-9.]+/ibm-aspera-connect-[0-9.]+-linux-.+\.tar.gz') \
      && aspera_connect_tarball="${aspera_connect_url##*/}" \
      && aspera_connect_install_script="${aspera_connect_tarball%.tar.gz}.sh" \
      && curl -o "${aspera_connect_tarball}" "${aspera_connect_url}" \
      && tar xzf ${aspera_connect_tarball} \
      && "./${aspera_connect_install_script}" \
      && cp /root/.aspera/connect/etc/*.* /etc/ \
      && cp /root/.aspera/connect/bin/* /usr/local/bin

RUN useradd data

USER data

CMD ["/bin/bash"]