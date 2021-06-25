FROM centos

MAINTAINER MAINTAINER Abhishek <abhishekbhardwaj510@gmail.com>

ENV DATA_VERSION=1.6.0 \
    FLUENTD_VERSION=0.12.42 \
    FLUENTD_ES=1.13.0-1 \
    FLUENTD_KUBE_METADATA=1.0.1-1 \
    FLUENTD_REWRITE_TAG=1.5.6-1 \
    FLUENTD_SECURE_FWD=0.4.5-2 \
    FLUENTD_SYSTEMD=0.0.9-1 \
    FLUENTD_VIAQ_DATA_MODEL=0.0.13 \
    FLUENTD_AUDIT_LOG_PARSER_VERSION=0.0.5 \
    FLUENTD_RECORD_MODIFIER=0.6.1 \
    GEM_HOME=/opt/app-root/src \
    HOME=/opt/app-root/src \
    PATH=/opt/app-root/src/bin:/opt/app-root/bin:/usr/libexec/fluentd/bin:$PATH \
    RUBY_VERSION=2.0 \
    OCP_OPERATIONS_PROJECTS='default openshift openshift-'

ARG TEST_REPO

RUN   yum install -y --setopt=tsflags=nodocs \
      gcc-c++ \
      ruby \
      ruby-devel \
      libcurl-devel \
      make \
      bc \
      iproute \
      autoconf automake libtool m4 \
      redhat-rpm-config && \
    yum clean all

RUN mkdir -p ${HOME} && mkdir -p /etc/fluent/plugin && \
    gem install -N --conservative --minimal-deps --no-ri --no-doc \
     'activesupport:<5' \
     'public_suffix:<3' \
     'elasticsearch-transport:<6' \
     'elasticsearch-api:<6' \
     'elasticsearch:<6' \
      fluentd:${FLUENTD_VERSION} \
     'fluent-plugin-elasticsearch:<2.0.0' \
     'fluent-plugin-kubernetes_metadata_filter:<1.1.0' \
      'fluent-plugin-record-modifier:<1.0.0' \
      'fluent-plugin-rewrite-tag-filter:<1.6.0' \
      fluent-plugin-secure-forward \
     'fluent-plugin-systemd:<0.1.0' \
      fluent-plugin-viaq_data_model \
     'fluent-plugin-remote-syslog:1.1' \
     'fluent-plugin-prometheus:<1.0.0'

ADD configs.d/ /etc/fluent/configs.d/
ADD filter_k8s_meta_for_mux_client.rb /etc/fluent/plugin/
ADD out_syslog_buffered.rb out_syslog.rb out_rawtcp.rb /etc/fluent/plugin/
ADD parser_viaq_docker_audit.rb viaq_docker_audit.rb /etc/fluent/plugin/
ADD run.sh generate_throttle_configs.rb generate_syslog_config.rb ${HOME}/

RUN mkdir -p /etc/fluent/configs.d/{dynamic,user} && \
    chmod -R 777 /etc/fluent && \
    chmod -R 777 /var/lib/ && \
    chmod 777 /etc/fluent/configs.d/dynamic && \
    ln -s /etc/fluent/configs.d/user/fluent.conf /etc/fluent/fluent.conf

WORKDIR ${HOME}

CMD ["sh", "run.sh"]

LABEL io.k8s.display-name=Fluentd

EXPOSE 24224

EXPOSE 24231
