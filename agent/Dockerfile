FROM oberthur/docker-ubuntu:16.04-20170303

MAINTAINER Dawid Malinowski <d.malinowski@oberthur.com>

ENV FLUENTD_VERSION=2.3.5

RUN curl https://packages.treasuredata.com/GPG-KEY-td-agent | apt-key add - \
  # add treasure data repository to apt
  && echo "deb http://packages.treasuredata.com/2/ubuntu/xenial/ xenial contrib" > /etc/apt/sources.list.d/treasure-data.list \

  # update your sources
  && apt-get update \

  # install deps
  && apt-get install -y make g++ git-core \

  # install the toolbelt
  && apt-get install -y td-agent=${FLUENTD_VERSION}* \

  # Change the default user and group to root.
  # Needed to allow access to /var/log/docker/... files.
  && sed -i -e "s/USER=td-agent/USER=root/" -e "s/GROUP=td-agent/GROUP=root/" /etc/init.d/td-agent \

  # https://github.com/repeatedly/fluent-plugin-record-modifier
  && td-agent-gem install --no-document fluent-plugin-record-modifier -v 0.5.0 \

  # https://github.com/fabric8io/fluent-plugin-kubernetes_metadata_filter
  && td-agent-gem install --no-document fluent-plugin-kubernetes_metadata_filter -v 0.27.0 \

  # https://github.com/kazegusuri/fluent-plugin-stdout-pp
  && td-agent-gem install --no-document fluent-plugin-stdout-pp -v 0.1.0 \

  # https://github.com/y-ken/fluent-plugin-rewrite-tag-filter
  && td-agent-gem install --no-document fluent-plugin-rewrite-tag-filter -v 1.5.6 \

  # https://github.com/gmr/fluent-plugin-json-in-json
  && td-agent-gem install fluent-plugin-json-in-json -v 0.1.4 \

  # https://github.com/fabric8io/fluent-plugin-docker_metadata_filter
  && td-agent-gem install --no-document fluent-plugin-docker_metadata_filter -v 0.1.3 \

  # clean deps
  && apt-get purge -y make g++ git-core \

  # clean up
  && apt-get clean autoclean \
  && apt-get autoremove --yes \
  && rm -rf /var/lib/{apt,dpkg,cache,log}/ \
  && rm -fr /tmp/* /var/tmp/*

ENV LD_PRELOAD=/opt/td-agent/embedded/lib/libjemalloc.so

# https://info.varnish-software.com/blog/understanding-varnish-cache-memory-usage
RUN ln -s 'lg_dirty_mult:8,lg_chunk:18' /etc/malloc.conf

# Run the Fluentd service.
ENTRYPOINT ["td-agent"]
