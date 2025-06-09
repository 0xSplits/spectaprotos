# spectaprotos

This is the API schema for the Specta RPC. The schema here describes how RPC
calls are shaped and function using [Protocol Buffer] definitions. Having a
unified abstraction helps us to generate client and server code across different
languages so that we remain mostly independent of transport layer specifics.

### Metrics

Specta follows a simple [Data Model] for unifying distributed observations as if
they occured in one place. The following methods are supported.

- Counter, the given value increments the relative representation of the underlying metric.
- Gauge, the given value defines the absolute representation of the underlying metric.
- Histogram, the given value expands the bucketed representation of the underlying metric.

### Limitations

All RPCs implement a hard limit on the maximum amount of actions that can be
processed within the same request. Specifically no more than 100 actions can be
received on any given endpoint in a single call.

### Development

Merging changes into the `main` branch triggers several Github Actions to auto
generate code for different programming languages. Once the package that you are
interested in is synchronized, you can import your updated dependency.

- `.github/workflows/pbf-go.yaml` updates https://github.com/0xSplits/spectagocode
- `.github/workflows/pbf-ts.yaml` updates https://github.com/0xSplits/spectatscode

### Formatting

You need to install the Clang Formatter on your system in order to format the
`.proto` files properly. If you are using VS Code you can also install the [VS
Code Extension] and format files on save.

```bash
brew install clang-format
```

```bash
clang-format -i $(find ./pbf -name "*.proto")
```

[Data Model]: https://opentelemetry.io/docs/specs/otel/metrics/data-model/#timeseries-model
[Protocol Buffer]: https://protobuf.dev
[VS Code Extension]: https://marketplace.visualstudio.com/items?itemName=xaver.clang-format
