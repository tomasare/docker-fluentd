FROM oberthur/docker-ubuntu:16.04-20170303

MAINTAINER Dawid Malinowski <d.malinowski@oberthur.com>

ENV FLUENTD_VERSION=2.3.5

RUN curl https://packages.treasuredata.com/GPG-KEY-td-agent | apt-key add - \
  # add treasure data repository to apt
  && echo "deb http://packages.treasuredata.com/2/ubuntu/xenial/ xenial contrib" > /etc/apt/sources.list.d/treasure-data.list \

  # update your sources
  && apt-get update \

  # install the toolbelt
  && apt-get install -y td-agent=${FLUENTD_VERSION}* \

  # Change the default user and group to root.
  # Needed to allow access to /var/log/docker/... files.
  && sed -i -e "s/USER=td-agent/USER=root/" -e "s/GROUP=td-agent/GROUP=root/" /etc/init.d/td-agent \

  # https://github.com/tagomoris/fluent-plugin-parser
  && td-agent-gem install --no-document fluent-plugin-parser -v 0.6.1 \

  # https://github.com/toyama0919/fluent-plugin-formatter_sprintf
  && td-agent-gem install --no-document fluent-plugin-formatter_sprintf -v 0.0.4 \

  # https://github.com/tagomoris/fluent-plugin-forest
  && td-agent-gem install --no-document fluent-plugin-forest -v 0.3.3 \

  # https://github.com/algas/fluent-plugin-retag
  && td-agent-gem install --no-document fluent-plugin-retag -v 0.0.1 \

  # https://github.com/dlackty/fluent-plugin-remote_syslog
  && td-agent-gem install --no-document fluent-plugin-remote_syslog -v 0.3.3 \

  # https://github.com/kazegusuri/fluent-plugin-stdout-pp
  && td-agent-gem install --no-document fluent-plugin-stdout-pp -v 0.1.0 \

  # https://github.com/uken/fluent-plugin-elasticsearch
  && td-agent-gem install --no-document fluent-plugin-elasticsearch -v 1.9.3 \

  # https://github.com/sonots/fluent-plugin-copy_ex
  && td-agent-gem install --no-document fluent-plugin-copy_ex -v 0.0.3 \

  # https://github.com/tagomoris/fluent-plugin-flowcounter
  && td-agent-gem install --no-document fluent-plugin-flowcounter -v 0.4.2 \

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
