FROM stonevil/debian-base
MAINTAINER stonevil@gmail.com

ENV CHRONOGRAF_VERSION=${CHRONOGRAF_VERSION:-0.12.0}
ENV CHRONOGRAF_DOWNLOAD_URL=https://dl.influxdata.com/chronograf/releases/chronograf_${CHRONOGRAF_VERSION}_amd64.deb

LABEL com.stonevil.chronograf.version=${CHRONOGRAF_VERSION}

RUN ${APT_UPDATE_CMD} && ${APT_UPGRADE_CMD} && \
  cd /tmp && \
  ${SOFTWARE_DOWNLOAD_CMD} ${CHRONOGRAF_DOWNLOAD_URL} -O && \
  dpkg -i chronograf_${CHRONOGRAF_VERSION}_amd64.deb && \
  ${APT_CACHE_RM} && \
  usermod -d /data/chronograf -s /bin/bash chronograf

ADD _rootfs /
ONBUILD ADD _rootfs_vendor /

EXPOSE 10000

VOLUME ["/data/chronograf"]

ENV PATH /opt/chronograf:$PATH

CMD mkdir -p /data/chronograf && chown -Rf chronograf /data/chronograf && \
  gosu chronograf chronograf -config /etc/chronograf/chronograf.conf
