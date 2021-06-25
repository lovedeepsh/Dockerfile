FROM centos:latest

LABEL maintainer "Abhishek <abhishek.dubey@opstree.com>"

ENV EXPORTERVERSION 0.12.0

ADD https://github.com/prometheus/alertmanager/releases/download/v${EXPORTERVERSION}/alertmanager-${EXPORTERVERSION}.linux-amd64.tar.gz /tmp/

RUN tar -xvzf /tmp/alertmanager-${EXPORTERVERSION}.linux-amd64.tar.gz -C /opt/ && \
    rm -rf /tmp/alertmanager-${EXPORTERVERSION}.linux-amd64.tar.gz && \
    cp /opt/alertmanager-${EXPORTERVERSION}.linux-amd64/amtool /bin/ && \
    cp /opt/alertmanager-${EXPORTERVERSION}.linux-amd64/alertmanager /bin/ && \
    chmod +x /bin/alertmanager && \
    chmod + /bin/amtool &&\
    mkdir /etc/alertmanager/  && \
    mv /opt/alertmanager-${EXPORTERVERSION}.linux-amd64/simple.yml /etc/alertmanager/config.yml

EXPOSE 9093

VOLUME [ "/alertmanager" ]

WORKDIR /alertmanager

ENTRYPOINT [ "/bin/alertmanager" ]

CMD        [ "--config.file=/etc/alertmanager/config.yml", \
             "--storage.path=/alertmanager" ]