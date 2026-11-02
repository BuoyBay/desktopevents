---
title: "desktopevents typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["DesktopEventKind", "DesktopEventMonitor", "DesktopEventRecord", "DesktopEventsLinuxDesktopEvent", "DesktopEventsLinuxDesktopMonitor", "DesktopEventsLinuxNativePropertyEvent", "DesktopEventsWindowsDesktopEvent", "DesktopEventsWindowsDesktopMonitor", "DesktopEventsWindowsNativeMessage"]
dependencies: []
symbols: ["DesktopEventKind", "DesktopEventMonitor", "DesktopEventRecord", "DesktopEventsLinuxDesktopEvent", "DesktopEventsLinuxDesktopMonitor", "DesktopEventsLinuxNativePropertyEvent", "DesktopEventsWindowsDesktopEvent", "DesktopEventsWindowsDesktopMonitor", "DesktopEventsWindowsNativeMessage"]
related: ["api.md", "getting-started.md", "index.md"]
---

# desktopevents typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## DesktopEventKind

`Public Enum DesktopEventKind As Integer`

### Values

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Other` | `DesktopEventKind` | `0` | — |
| `ActiveWindowChanged` | `DesktopEventKind` | `1` | — |
| `WorkspaceChanged` | `DesktopEventKind` | `2` | — |
| `WindowListChanged` | `DesktopEventKind` | `3` | — |

## DesktopEventRecord

`Public Class DesktopEventRecord`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Kind` | `DesktopEventKind` | Yes | No | — | — |
| `NativeName` | `String` | Yes | No | — | — |
| `WindowId` | `Integer` | Yes | No | — | — |
| `TimestampMilliseconds` | `Integer` | Yes | No | — | — |
| `IsSynthetic` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(vKind As DesktopEventKind, vNativeName As String, vWindowId As Integer, vTimestampMilliseconds As Integer, vIsSynthetic As Boolean)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `vKind` | `DesktopEventKind` | `ByVal` | Required |
| `vNativeName` | `String` | `ByVal` | Required |
| `vWindowId` | `Integer` | `ByVal` | Required |
| `vTimestampMilliseconds` | `Integer` | `ByVal` | Required |
| `vIsSynthetic` | `Boolean` | `ByVal` | Required |

Returns: no value.

### DesktopEventsSupported

`Public Function DesktopEventsSupported() As Boolean`

Read-only compile-target backend test; no runtime I/O.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### DesktopEventsAvailable

`Public Function DesktopEventsAvailable() As Boolean`

Read-only: Linux opens/closes an X display; Windows probes user32/kernel32. No monitor is installed.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

## DesktopEventMonitor

`Public Class DesktopEventMonitor`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Backend` | `String` | Yes | No | — | — |
| `DroppedEventCount` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(capacity As Integer = 256)`

Read-only event subscription, on the creating thread. Windows permits one live monitor per process.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `capacity` | `Integer` | `ByVal` | `256` |

Returns: no value.

### Drain

`Public Function Drain(limit As Integer = 256) As Array Of DesktopEventRecord`

Read-only, bounded drain (1..65536). Pumps at most 64 Windows messages or consumes 4096 X events; never waits for an event.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `limit` | `Integer` | `ByVal` | `256` |

#### Returns

| Type |
| --- |
| `Array Of DesktopEventRecord` |

### Close

`Public Sub Close()`

Releases the subscription on its creating thread; idempotent. No callbacks are delivered after successful close.

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.

## DesktopEventsLinuxDesktopEvent

`Public Class DesktopEventsLinuxDesktopEvent`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `PropertyName` | `String` | No | No | — | — |
| `WindowId` | `UInt64` | No | No | — | — |
| `TimestampMilliseconds` | `UInt64` | No | No | — | — |
| `IsDeleted` | `Boolean` | No | No | — | — |
| `IsSynthetic` | `Boolean` | No | No | — | — |
| `IsActiveWindowChange` | `Boolean` | No | No | — | — |
| `IsWorkspaceChange` | `Boolean` | No | No | — | — |
| `IsWindowListChange` | `Boolean` | No | No | — | — |

## DesktopEventsLinuxNativePropertyEvent

`Sequential Structure DesktopEventsLinuxNativePropertyEvent`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `EventType` | `Int32` | — | — |
| `Serial` | `UInt64` | — | — |
| `SendEvent` | `Int32` | — | — |
| `DisplayHandle` | `Ptr` | — | — |
| `WindowId` | `UInt64` | — | — |
| `AtomId` | `UInt64` | — | — |
| `EventTime` | `UInt64` | — | — |
| `EventState` | `Int32` | — | — |

### DesktopEventsLinuxIsSupported

`Public Function DesktopEventsLinuxIsSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### DesktopEventsLinuxIsAvailable

`Public Function DesktopEventsLinuxIsAvailable() As Boolean`

Probe the default X display; this does not claim native Wayland support.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

## DesktopEventsLinuxDesktopMonitor

`Public Class DesktopEventsLinuxDesktopMonitor`

### Constructor

`Public Sub Constructor()`

No parameters.

Returns: no value.

### Close

`Public Sub Close()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.

### Drain

`Public Function Drain(limit As Integer = 256) As Array Of DesktopEventsLinuxDesktopEvent`

Drain at most limit queued events; never waits for a new event.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `limit` | `Integer` | `ByVal` | `256` |

#### Returns

| Type |
| --- |
| `Array Of DesktopEventsLinuxDesktopEvent` |

## DesktopEventsWindowsDesktopEvent

`Public Class DesktopEventsWindowsDesktopEvent`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `EventId` | `Integer` | No | No | — | — |
| `WindowHandle` | `Ptr` | No | No | — | — |
| `ObjectId` | `Integer` | No | No | — | — |
| `ChildId` | `Integer` | No | No | — | — |
| `SourceThreadId` | `Integer` | No | No | — | — |
| `EventTimeMilliseconds` | `Integer` | No | No | — | — |

## DesktopEventsWindowsNativeMessage

`Sequential Structure DesktopEventsWindowsNativeMessage`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `WindowHandle` | `Ptr` | — | — |
| `MessageId` | `UInt32` | — | — |
| `WordParameter` | `UInt64` | — | — |
| `LongParameter` | `Int64` | — | — |
| `Time` | `UInt32` | — | — |
| `PointX` | `Int32` | — | — |
| `PointY` | `Int32` | — | — |
| `PrivateValue` | `UInt32` | — | — |

### DesktopEventsWindowsIsSupported

`Public Function DesktopEventsWindowsIsSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

## DesktopEventsWindowsDesktopMonitor

`Public Class DesktopEventsWindowsDesktopMonitor`

### Constructor

`Public Sub Constructor(firstEvent As Integer = 3, lastEvent As Integer = 3, processId As Integer = 0, capacity As Integer = 256)`

Default watches EVENT_SYSTEM_FOREGROUND on the current desktop.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `firstEvent` | `Integer` | `ByVal` | `3` |
| `lastEvent` | `Integer` | `ByVal` | `3` |
| `processId` | `Integer` | `ByVal` | `0` |
| `capacity` | `Integer` | `ByVal` | `256` |

Returns: no value.

### Pump

`Public Sub Pump(maxMessages As Integer = 64)`

For console loops. GUI applications may use their existing message loop.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `maxMessages` | `Integer` | `ByVal` | `64` |

Returns: no value.

### DrainEvents

`Public Function DrainEvents() As Array Of DesktopEventsWindowsDesktopEvent`

No parameters.

#### Returns

| Type |
| --- |
| `Array Of DesktopEventsWindowsDesktopEvent` |

### DroppedEventCount

`Public Function DroppedEventCount() As Integer`

No parameters.

#### Returns

| Type |
| --- |
| `Integer` |

### Close

`Public Sub Close()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.
