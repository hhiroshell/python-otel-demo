# python-otel-demo
https://logz.io/blog/python-opentelemetry-auto-instrumentation/
https://opentelemetry.io/docs/instrumentation/python/getting-started/

- preparation

```
$ pip install -r requirements.txt && opentelemetry-bootstrap -a install
```

- run the instrumented app and have it print telemetries to the console

```
$ opentelemetry-instrument \
    --traces_exporter console \
    --metrics_exporter console \
    python3 server.py

# from another terminal
$ curl localhost:81
```

- with local otel-collector

```
# download and run local otel-colletor
$ OTEL_COLECTOR_RELEASES="https://github.com/open-telemetry/opentelemetry-collector-releases"

$ curl -L ${OTEL_COLECTOR_RELEASES}/releases/download/v0.87.0/otelcol-contrib_0.87.0_linux_amd64.tar.gz | tar xz

$ ./otelcol-contrib --config ./collector-conifg.yaml

# from another terminal
$ export OTEL_TRACES_EXPORTER=otlp && \
  export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317" && \
  export OTEL_RESOURCE_ATTRIBUTES="service.name=test" && \
  export OTEL_METRICS_EXPORTER=""

$ opentelemetry-instrument python3 server.py
```
