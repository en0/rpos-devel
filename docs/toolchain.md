# Toolchain

RPOS requires a compiler, linker, and assembler that is capable of producing
output that RPOS can understand. In this case we are talking about a
cross-compiler, a compiler that runs on one platform but builds output for a
diffrent platform.

The RPOS Toolchain is the [GNU Compiler Collection](https://www.gnu.org/software/gcc/)
and [Binutils](https://www.gnu.org/software/binutils/) linked against a ported
version of [Red Hat's Newlib](https://sourceware.org/newlib/) standard C 
library. Both GCC/Binutils and Newlib have been modified to add a custom target
for i686-rpos. You can obtain these modified versions of the software from
these locations:

- [rpos-binutils](https://github.com/en0/rpos-binutils)
- [rpos-gcc](https://github.com/en0/rpos-gcc)
- [rpos-newlib](https://github.com/en0/rpos-newlib)

## Prerequisites

The following libraries must be installed installed in the host environment.
Most should be available through your system's package manager.

- GCC
- GNU Make
- GNU Bison
- Flex
- GNU GMP
- GNU MPFR
- GNU MPC
- texinfo
- automake
- autoconf (exactly version 2.64)
- libtool

## Building

Follow these steps to build the RPOS Toolchain cross-compiler.

1. Verify all the submodules for this project are cloned.

```bash
git submodule update --init --recursive
```
 
2. Import the i686-elf profile.

``` bash
source tools/profile-i686-elf.env
```

3. Build Binutils for a generic elf target.

```bash
cd system/host/src/rpos-binutils && ./xbuild.sh && cd -
```

4. Build GCC for a generic elf target.

```bash
cd system/host/src/rpos-gcc && ./xbuild.sh && cd -
```

5. Import the os specific target.

```bash
profile-switch profile-i686-rpos
```

6. Create symlinks to satisfy newlib's build system

```bash
cd system/host/bin && for BIN in ar as gcc ranlib; do ln -s i686-elf-$BIN $TARGET-$BIN; done && ln -s i686-elf-gcc $TARGET-cc && cd -
```

7. Build Newlib.

```bash
cd system/host/src/rpos-newlib && ./xbuild.sh && cd -
```

8. Remove the symlinks used to build newlib.

```bash
find system/host/bin -type l | xargs -n1 unlink
```

9. Rebuild Binutils for the OS Specific target

```bash
cd system/host/src/rpos-binutils && ./xbuild.sh && cd -
```

10. Rebuild Gcc for the OS Specific target

```bash
cd system/host/src/rpos-gcc && ./xbuild.sh && cd -
```
