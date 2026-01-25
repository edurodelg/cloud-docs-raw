---
source_url: https://google.github.io/adk-docs/streaming/configuration/
fetched_at: 2026-01-25T15:09:26.227539
---

# Configuring streaming behaviour¶

# Configuring streaming behaviour[¶](#configuring-streaming-behaviour)

Supported in ADKPython v0.5.0Experimental

There are some configurations you can set for live(streaming) agents.

It's set by [RunConfig](https://github.com/google/adk-python/blob/main/src/google/adk/agents/run_config.py). You should use RunConfig with your [Runner.run_live(...)](https://github.com/google/adk-python/blob/main/src/google/adk/runners.py).

For example, if you want to set voice config, you can leverage speech_config.