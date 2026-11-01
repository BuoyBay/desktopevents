---
title: "Getting started with desktopevents"
summary: "Import desktopevents, check platform availability, and handle results and failures."
category: "Guide"
order: 10
keywords: ["desktopevents", "DesktopEvents", "native", "events"]
symbols: ["DesktopEventMonitor", "DesktopEventRecord", "DesktopEventKind", "DesktopEventsSupported", "DesktopEventsAvailable"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

Install `desktopevents` into your project’s packages directory with your package workflow, then import `desktopevents`. Use the DesktopEvents facade instead of importing platform backend modules.

Check `DesktopEventsSupported()` and `DesktopEventsAvailable()` before constructing `DesktopEventMonitor`. Choose a queue capacity from 1 through 65536; the default is 256. On the creating thread, periodically call `Drain()` or `Drain(limit)` and consume its `Array Of DesktopEventRecord`. Check `DroppedEventCount` to detect observed queue loss and explicitly call `Close()` on that same thread when finished.

## Handling availability

A Supported predicate describes the compile target. An Available predicate probes runtime prerequisites; it does not guarantee that the next operation will succeed. Preserve the distinction between successful empty results and an exception. Consult the [API contracts](api.md) for supported platforms, blocking behavior, and lifecycle requirements.

The [typed reference](typed-api.md) lists argument types, defaults, read-only properties, and return values. It also includes declarations from internal backend source modules; applications should use the facade entry points described here.
