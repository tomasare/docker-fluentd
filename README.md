# docker-fluentd

Fluentd types:
- **agent** - runs on kubernetes nodes or nodes based on 2.0.6 ( docker-commpose ) and forwards all logs to routers
- **router** - forwards logs based on tag/destination to specific agents
- **backend** - there are few types like: audit, elastic and file. They are final step to write logs to specific destinations

```
agent -> router -> backend
```

|plugin / mode|version|backend|router|agent|
|---|:---:|:---:|:---:|:---:|
|[fluent-plugin-parser](https://github.com/tagomoris/fluent-plugin-parser)                                          |0.6.1|+|-|-|
|[fluent-plugin-formatter_sprintf](https://github.com/toyama0919/fluent-plugin-formatter_sprintf)                   |0.0.4|+|-|-|
|[fluent-plugin-forest](https://github.com/tagomoris/fluent-plugin-forest)                                          |0.3.3|+|-|-|
|[fluent-plugin-retag](https://github.com/algas/fluent-plugin-retag)                                                |0.0.1|+|-|-|
|[fluent-plugin-remote_syslog](https://github.com/dlackty/fluent-plugin-remote_syslog)                              |**0.3.2**|+|-|-|
|[fluent-plugin-copy_ex](https://github.com/sonots/fluent-plugin-copy_ex)                                           |0.0.3|-|+|-|
|[fluent-plugin-record-modifier](https://github.com/repeatedly/fluent-plugin-record-modifier)                       |0.5.0|-|-|+|
|[fluent-plugin-kubernetes_metadata_filter](https://github.com/fabric8io/fluent-plugin-kubernetes_metadata_filter)  |0.27.0|-|-|+|
|[fluent-plugin-stdout-pp](https://github.com/kazegusuri/fluent-plugin-stdout-pp)                                   |0.1.0|+|+|+|
|[fluent-plugin-rewrite-tag-filter](https://github.com/y-ken/fluent-plugin-rewrite-tag-filter)                      |1.5.6|-|-|+|
|[fluent-plugin-json-in-json](https://github.com/gmr/fluent-plugin-json-in-json)                                    |**0.1.4**|-|-|+|
|[fluent-plugin-elasticsearch](https://github.com/uken/fluent-plugin-elasticsearch)                                 |**1.9.3**|+|-|-|
|[fluent-plugin-docker_metadata_filter](https://github.com/fabric8io/fluent-plugin-docker_metadata_filter)          |0.1.3|-|-|+|
|[fluent-plugin-flowcounter](https://github.com/tagomoris/fluent-plugin-flowcounter)          |0.4.2|-|+|-|
