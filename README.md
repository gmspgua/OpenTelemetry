# OpenTelemetry Collector Demo

*IMPORTANT:* This is a pre-released version of the OpenTelemetry Collector Contrib.

This demo contains a client and server applications that use the
opentelemetry Go library for instrumentation and for sending telemetry data
to the opentelemetry collector.

The client periodically makes http calls to the server which
create client spans, server spans and metrics that track information like
number of http requests and latency.

This demo presents the typical flow of observability data with multiple
OpenTelemetry Collectors deployed:

- The client and server send data directly to the OTel Collector;
- The OTel Collector then sends the data to the appropriate backend, in this demo
 Jaeger, Zipkin, and Prometheus;

This demo uses `docker-compose` and by default runs against the 
`otel/opentelemetry-collector-contrib-dev:latest` image. To run the demo, switch
to the `examples/demo` folder and run:

```shell
docker-compose up -d
```


Steps:
```shell
1 - Create Token Authentication in Dynatrace UI, Access Token with scopes "apiTokens.write","openTelemetryTrace.ingest".
2 - Configure OTEL Agent in file otel-collector-config.yaml adding API Endpoint and Token created by previos step.
3 - Execute docker-compose up
4 - See the tracers span ingested into Dynatrace.
```
```shell
references:
https://www.dynatrace.com/support/help/extend-dynatrace/opentelemetry/opentelemetry-ingest#expand--sample-collector-configuration
https://www.dynatrace.com/support/help/extend-dynatrace/opentelemetry
```

Notes:

- It may take some time for the application metrics to appear on the Prometheus
 dashboard;

To clean up any docker container from the demo run `docker-compose down` from 
the `examples/demo` folder.

### Using a Locally Built Image
Developers interested in running a local build of the Collector need to build a
docker image using the command below:

```shell
make docker-otelcol
```

And set an environment variable `OTELCOL_IMG` to `otelcol:latest` before 
launching the command `docker-compose up -d`.
stop the command `docker-compose down`.


"# OpenTelemetry" 

![Untitled Diagram](https://user-images.githubusercontent.com/34476524/151684854-7297ad59-74fd-47be-87b5-664c54f41830.jpg)
