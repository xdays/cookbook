# OpenTelemetry Specification

## Overview

### Distributed Tracing

#### Trace

a directed acyclic graph of Spans, span relationship can be parent/child

```
Causal relationships between Spans in a single Trace

        [Span A]  ←←←(the root span)
            |
     +------+------+
     |             |
 [Span B]      [Span C] ←←←(Span C is a `child` of Span A)
     |             |
 [Span D]      +---+-------+
               |           |
           [Span E]    [Span F]
```

#### Span

1. Operation name
2. Start and finish timestamp
3. Attributes
4. Events
5. Parent's span identifier
6. Links to zero or more causually-related Span(via SpanContext of these related Spans)
7. SpanContext identification of a Span.

#### SpanContext

Represents all information that identifies Span in the Trace and must porpagated to child Spans across process bondaries

1. TraceId
2. SpanId
3. TraceFlags
4. Tracestate

#### Links between Spans

Links can be used to represent batched operations where a Span was initiated by multiple initiating Spans, each representing a single incoming item being processed in the batch.

Another example of using a Link is to declare the relationship between the originating and following trace

### Metrics

#### Raw Measurements

1. Measure
2. Measurement

#### Metrics with predefined aggregation

1. Counter
2. Gauge

### Logs

Log data model

### CorrelationContext

????

### Resources

Capture information about entity where temeletry is collected

### Propagators

Serialize and deserialize

### Collector

Collect traces, metrics and logs from processes

Can be deployed in two modes:

1. Agent
2. Standalone

### Instrumentation Libraries

Library that help existing libraries or frameworks to integrate with opentelemetry sdk
