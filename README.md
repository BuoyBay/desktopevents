# Active window and workspace events

Import `desktopevents` (or `desktopevents.DesktopEvents`). This focused package owns `DesktopEventsSupported()`, `DesktopEventsAvailable()` and `DesktopEventMonitor(capacity As Integer = 256)`. It has no package, container, or external source dependency. Backend modules are implementation details and are non-public imports; their module-scope symbols are globally prefixed to avoid collisions.

Enumeration is read-only. Empty arrays mean successful enumeration with no results; missing services/libraries, denied access and native errors throw. Missing optional fields are None, present empty strings are Some(""). No absent numeric or powered state is fabricated as zero/False. Snapshot properties are read-only owned copies. Native IDs are observations in their backend namespace, not cross-platform stable identities or openable handles.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add desktopevents --git https://github.com/BuoyBay/desktopevents.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## API entrypoints

- `DesktopEventsSupported()`
- `DesktopEventsAvailable()`
- `DesktopEventMonitor(capacity As Integer = 256)`
- `Drain(limit = 256)`

## Platform and scope

Backend support and event availability are separate capabilities. Check the source guide for the supported host/session and lifetime requirements.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer desktopevents
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```


## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
