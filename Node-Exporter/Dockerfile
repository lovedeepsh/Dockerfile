FROM centos:latest

LABEL maintainer "Abhishek <abhishek.dubey@opstree.com>"

ENV EXPORTERVERSION 0.16.0 

ADD https://github.com/prometheus/node_exporter/releases/download/v${EXPORTERVERSION}/node_exporter-${EXPORTERVERSION}.linux-amd64.tar.gz /tmp/

RUN tar -xvzf /tmp/node_exporter-${EXPORTERVERSION}.linux-amd64.tar.gz -C /opt/ && \
    rm -rf /tmp/node_exporter-${EXPORTERVERSION}.linux-amd64.tar.gz && \
    ln -s /opt/node_exporter-${EXPORTERVERSION}.linux-amd64/node_exporter /bin/node_exporter && \
    mkdir /etc/node_exporter && \
    chmod +x /bin/node_exporter

VOLUME     [ "/nodeexporter" ]

WORKDIR    /nodeexporter

ENTRYPOINT [ "/bin/node_exporter" ]

EXPOSE 9100
