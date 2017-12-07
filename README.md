# Prometheus-fast-remote-release

This is a bosh-release for [prometheus-fast-remote](https://github.com/orange-cloudfoundry/prometheus-fast-remote)

This release permit to use the remote adapter beside a prometheus through [prometheus-boshrelease](https://github.com/cloudfoundry-community/prometheus-boshrelease).


## Use it

This is quite straight forward to use it, only few properties has to be set:

```yml
properties:
  fast_remote.kairos_url:
    description: Url to target your kairosdb
    example: https://my.kairosdb.com
  fast_remote.skip_insecure:
    description: Set to true if you don't want to check certificates (not recommended)
    default: false
  fast_remote.listen_addr:
    description: Set the interface and port to listen for the remote server
    default: "0.0.0.0:9119"
  fast_remote.log_level:
    description: "Set log level (Values are: DEBUG, INFO, WARNING, ERROR and PANIC)"
    default: INFO
  fast_remote.log_json:
    description: Set to true to save logs in json format
    default: true
  fast_remote.workers:
    description: Set number of workers in the pool to write samples into the time serie database. 
    default: 10
```

You can now set a remote adapter in your prometheus deployment in this simple way:

```yml
properties:
  prometheus:
    remote_write:
    - url: "http://127.0.0.1:9119/write" # replace 127.0.0.1 by the correct ip where run fast_remote
    remote_read:
    - url: "http://127.0.0.1:9119/read" # replace 127.0.0.1 by the correct ip where run fast_remote
```