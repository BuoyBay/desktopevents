---
title: "desktopevents API contracts"
summary: "Platform support, result semantics, and operational constraints for desktopevents."
category: "Reference"
order: 20
keywords: ["desktopevents", "DesktopEvents", "native", "events"]
symbols: ["DesktopEventMonitor", "DesktopEventRecord", "DesktopEventKind", "DesktopEventsSupported", "DesktopEventsAvailable"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# desktopevents API contracts

## Platform support

Linux monitors X11 root PropertyNotify events. Windows uses out-of-context WinEvents. macOS is unsupported. The Linux availability probe opens and closes the default X display; the Windows probe checks user32 and kernel32. Neither probe installs a monitor. Construction explicitly subscribes; importing does not.

## Event meanings

| DesktopEventKind | X11 | Windows |
| --- | --- | --- |
| ActiveWindowChanged | _NET_ACTIVE_WINDOW | 0x0003 |
| WorkspaceChanged | _NET_CURRENT_DESKTOP | Not mapped |
| WindowListChanged | _NET_CLIENT_LIST or _NET_CLIENT_LIST_STACKING | 0x8000 or 0x8001, window object with child zero |
| Other | Other root properties | Not emitted by this mapping |

`DesktopEventRecord` is an owned read-only snapshot. `NativeName` records the property/event label. `WindowId` is an opaque numeric observation; never dereference it as a pointer. `TimestampMilliseconds` uses the native clock for ordering, not a shared wall clock. `IsSynthetic` reflects X11 send_event; Windows supplies no provenance bit, so False there does not establish physical user input.

## Queue and drain limits

`Drain(limit As Integer = 256)` accepts 1 through 65536, returns at most that many records, and retains the remainder. It never waits for a new event. Each call processes at most 4096 queued X events or 64 Windows messages. The owned queue drops newest events when full.

`DroppedEventCount` reports observed application/native-callback queue losses. It cannot measure all operating-system losses. Xlib’s upstream queue is outside the bounded application buffer. `Backend` is x11 or win32-winevent on supported targets.

## Thread ownership and close

Construction, `Drain`, `DroppedEventCount`, and `Close` belong to the creating thread. Windows permits one live monitor per process. `Close()` releases the subscription and is idempotent. Drain and dropped-count access after close throw `InvalidArgumentException`; invalid capacities and drain limits also throw that exception.

Use structured cleanup to call `Close()` explicitly on the owner thread, including when processing throws. Destruction catches errors and cannot safely release a subscription from another thread. Successful close ends callback delivery. Windows preserves WM_QUIT and prevents callback exceptions from unwinding through native frames. Xlib connection loss can still terminate the process.

[Full typed reference](typed-api.md) · [Getting started](getting-started.md)
