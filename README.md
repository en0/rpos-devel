# rpos

Research Project Operating System.

I have made many attempts and building an operating system and never achieved
my goal to satisfaction. After a significant amount of leanring and
continuously misplacing my code, I have decided to keep it as simple as
possible and then overcomplicated it.

If you are interested in contributing to this code or just want to play around
with it, take a look at [the documentation](docs/index.md).

## Goals

- [x] Kernel loads in higher half
- [x] Create flat GDT in kernel .text space
- [x] IDT gate install system where other code can install handlers
- [x] IRQ dispatch system where hardware handlers can install int handers.
- [x] Serial debuging on COM1
- [x] Coredump on FAULT/TRAP
- [x] RTC via PIT Channel 0
- [x] Setup physical memory manager
- [x] Setup Virtual memory manager
- [x] 8MB Stack just under the kernel in the virtual address space.
- [ ] Kernel will pull from it's own small heap at 0xC0400000
