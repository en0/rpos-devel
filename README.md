# rpos

Research Project Operating System Development Project.

This repo contains the file structure and documentation requried for developing
the RPOS orperating system. There is very little code in this project, it is
mostly a collection of submodules and centralized docs designed to aggregate
all the inforamtion into one place.

If you are interested in contributing to this code or just want to play around
with it, take a look at [the documentation](docs/index.md).

## File Layout

- docs: Contains RPOS documentation.
- tools: Contains scripts and env files for building and testing code.
- system: Contains a mock root file structure for RPOS which contains links to
  submodules.

## system root

The system directory contains all the code and the configuration for building
and testing RPOS.  The structure should look familure but there are subtle
diffrences.

### system/host

The host directory contains code and binaries that run in a externally hosted
environment (external to RPOS). These are things like the the GCC Cross
Compiler and tools to build initfs.

#### system/host/src

All the submodues that require building on an external host. This includes the
RPOS Kernel and other pre-install tooling like building initfs.

You can see the submodules under `system/host/src`

### system/usr

The usr directory contains code that intended to run inside RPOS after boot.
This is theoretical at the moment as RPOS cannot yet run the toolchain.

### system/etc

Contains configuration files that will be added to initfs for building the
kernel output and creating a bootable image.

## gitignore

Only the following directories under `system` are allowed to be tracked by
source control.

- system/etc
- system/src
- system/usr/src
- system/host/src

Note that there are no restructions on files above the system directory.

