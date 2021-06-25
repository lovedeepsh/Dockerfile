FROM ubuntu:latest

LABEL maintainer "Abhishek <abhishek.dubey@opstree.com>"

ENV GRAFANA_VERSION 4.6.3

ADD https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana_${GRAFANA_VERSION}_amd64.deb /tmp/

COPY ./run.sh /run.sh

RUN apt-get update && \
    apt-get -y --no-install-recommends install libfontconfig curl ca-certificates && \
    dpkg -i /tmp/grafana_${GRAFANA_VERSION}_amd64.deb && \
    rm -rf /tmp/grafana_${GRAFANA_VERSION}_amd64.deb && \
    curl -L https://github.com/tianon/gosu/releases/download/1.10/gosu-amd64 > /usr/sbin/gosu && \
    chmod +x /usr/sbin/gosu && \
    apt-get autoremove -y && \
    chmod +x /run.sh

VOLUME ["/var/lib/grafana", "/var/log/grafana", "/etc/grafana"]

EXPOSE 3000

ENTRYPOINT ["/run.sh"]