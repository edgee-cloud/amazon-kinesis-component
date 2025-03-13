<div align="center">
<p align="center">
  <a href="https://www.edgee.cloud">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://cdn.edgee.cloud/img/component-dark.svg">
      <img src="https://cdn.edgee.cloud/img/component.svg" height="100" alt="Edgee">
    </picture>
  </a>
</p>
</div>

<h1 align="center">Amazon Kinesis component for Edgee</h1>

[![Coverage Status](https://coveralls.io/repos/github/edgee-cloud/amazon-kinesis-component/badge.svg)](https://coveralls.io/github/edgee-cloud/amazon-kinesis-component)
[![GitHub issues](https://img.shields.io/github/issues/edgee-cloud/amazon-kinesis-component.svg)](https://github.com/edgee-cloud/amazon-kinesis-component/issues)
[![Edgee Component Registry](https://img.shields.io/badge/Edgee_Component_Registry-Public-green.svg)](https://www.edgee.cloud/edgee/amazon-kinesis)

This component enables seamless integration between [Edgee](https://www.edgee.cloud) and [Amazon Kinesis](https://aws.amazon.com/kinesis/), allowing you to collect and forward analytics events to your streaming pipelines.


## Quick Start

1. Download the latest component version from our [releases page](../../releases)
2. Place the `kinesis.wasm` file in your server (e.g., `/var/edgee/components`)
3. Add the following configuration to your `edgee.toml`:

```toml
[[destinations.data_collection]]
id = "kinesis"
file = "/var/edgee/components/kinesis.wasm"
settings.aws_access_key = "YOUR_AWS_ACCESS_KEY"
settings.aws_secret_key = "YOUR_AWS_SECRET_KEY"
settings.aws_region = "YOUR_AWS_REGION"
settings.kinesis_stream = "YOUR_STREAM_NAME_OR_ARN"
```


## Event Handling

### Event Mapping
The component maps Edgee events to Kinesis records as follows:

| Edgee Event | Kinesis record | Description |
|-------------|----------------|-------------|
| Page        | `full-event.json` | Full JSON dump of the Page event |
| Track       | `full-event.json` | Full JSON dump of the Track event |
| User        | `full-event.json` | Full JSON dump of the User event |


## Configuration Options

### Basic Configuration
```toml
[[destinations.data_collection]]
id = "kinesis"
file = "/var/edgee/components/kinesis.wasm"
settings.aws_access_key = "YOUR_AWS_ACCESS_KEY"
settings.aws_secret_key = "YOUR_AWS_SECRET_KEY"
settings.aws_region = "YOUR_AWS_REGION"
settings.kinesis_stream = "YOUR_STREAM_NAME_OR_ARN"

# Optional configurations
settings.aws_session_token = "YOUR_AWS_SESSION_TOKEN" # Useful for tests, not recommended in prod since it's short-lived
settings.kinesis_partition = "static-partition-key" # Optional, used for all PutRecord calls
```


### Event Controls
Control which events are forwarded to Amazon Kinesis:
```toml
settings.edgee_page_event_enabled = true   # Enable/disable page view tracking
settings.edgee_track_event_enabled = true  # Enable/disable custom event tracking
settings.edgee_user_event_enabled = true   # Enable/disable user identification
```


## Development

### Building from Source
Prerequisites:
- [Rust](https://www.rust-lang.org/tools/install)
- wit-deps: `cargo install wit-deps`

Build command:
```bash
make build
```

Test command:
```bash
make test
```

Test coverage command:
```bash
make test.coverage[.html]
```

### Contributing
Interested in contributing? Read our [contribution guidelines](./CONTRIBUTING.md)

### Security
Report security vulnerabilities to [security@edgee.cloud](mailto:security@edgee.cloud)
