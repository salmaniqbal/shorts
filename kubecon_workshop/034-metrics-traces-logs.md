# 034 - Metrics, Traces, Logs: Stop Making AI Guess

_Workshop: Break It, Watch It, Fix It (with a little AI help). Body ~38 seconds, plus an 8-second outro._

## Script

You ask an AI why checkout is slow. It blames the database. The database is fine.

It wasn't lying. It was guessing, because all you gave it was logs.

You need three signals, in order.

Metrics tell you *that* something's wrong: checkout latency just tripled.

Traces tell you *where*: two seconds of every request is spent waiting on payments.

Logs tell you *why*: payments keeps retrying a call that times out.

The trick that joins them up? Put the trace ID in every log line, so a slow trace leads you straight to its logs.

That works for you, and it works for AI. Give it evidence, not a hunch.

Instrument a broken app and debug it with AI in our KubeCon workshop, Break It, Watch It, Fix It. Link below.

## On-screen Snippet

```json
{
  "level": "warn",
  "service": "payments",
  "msg": "bank-api timeout after 500ms, attempt 2/4",
  "trace_id": "4bf92f3577b34da6a3ce929d0e0e4736"
}
```

## Notes
- Use the numbers consistently on screen. Metrics: p99 goes from 0.8s to 2.4s. Trace: 2.4s in total, of which payments takes 2.0s. Logs: 4 attempts × 500ms timeout = the missing 2 seconds.
- OpenTelemetry can inject `trace_id` and `span_id` into your logs for you: the Java agent does it through MDC, and Python does it with `OTEL_PYTHON_LOG_CORRELATION=true`. Most log backends then let you click from a trace to its logs.
- This works anywhere, not just in Kubernetes: VMs, serverless, a monolith on one box.
- When you ask an LLM to debug, paste the metric, the trace and the correlated logs together. One log file on its own invites a confident guess.
- `4bf92f3577b34da6a3ce929d0e0e4736` is the example trace ID from the W3C Trace Context spec, so it's safe to show.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "You ask an AI why checkout is slow" | Chat UI: "Why is checkout slow?" |
| "It blames the database" | Robot: "It's the database. Definitely the database." with a "98% confident" badge |
| "The database is fine" | Postgres card: green HEALTHY, `p99 4ms · CPU 12%`, then a red WRONG stamp over the AI's answer |
| "It wasn't lying" | Robot looking innocent |
| "It was guessing" | Robot squinting at a wall of scrolling grey log lines |
| "all you gave it was logs" | File icon `logs.txt` being handed over, nothing else |
| "three signals" | Three tiles pop in: 1 METRICS (blue), 2 TRACES (purple), 3 LOGS (amber) |
| "Metrics tell you *that*" | Line chart for checkout p99, flat then a sharp spike, counter ticking 0.8s -> 2.4s, then "×3" |
| "Traces tell you *where*" | Trace waterfall: checkout 2.4s, cart 140ms, inventory 160ms, payments 2.0s bar growing long and red |
| "waiting on payments" | Arrow onto the payments span: "2.0s of 2.4s" |
| "Logs tell you *why*" | Payments log terminal: `WARN bank-api timeout 500ms, attempt 1/4` ... 2/4 ... 3/4 ... `INFO ok on attempt 4` |
| "keeps retrying a call that times out" | `4 × 500ms = 2s` pops beside the logs |
| "The trick that joins them up" | Metrics, traces and logs tiles with a chain linking them |
| "trace ID in every log line" | JSON log line from the snippet above, `trace_id` highlighted |
| "a slow trace leads you straight to its logs" | Click on the payments span -> jumps to the four matching log lines, the same trace ID glowing on both |
| "works for AI" | Robot again, now correct: "Payments retries a bank-api call that times out. 4 × 500ms = 2s." with chips: metric ✓ trace ✓ logs ✓ |
| "evidence, not a hunch" | Big text: "Evidence, not hunches." |
| "KubeCon workshop" | End card: "Break It," (red) "Watch It," (amber) "Fix It" (green), "(with a little AI help)", "Link below ↓" |

## Meme Opportunity
- "It's always DNS" / AI: "It's always the database"
- Charlie Day conspiracy board, labelled "debugging with logs only"
- Detective meme: metrics = "a crime happened", traces = "in the payments room", logs = "with a timeout"
