# ruyos

A minimal x86_64 operating system kernel written from scratch in Assembly and C.

- Multiboot2 header and 32-bit entry point (`src/impl/x86_64/boot/main.asm`)
- CPU checks (CPUID, long mode support), page table setup and paging (`main.asm`)
- Switch to 64-bit long mode and jump into the C kernel (`main64.asm`)
- Freestanding C kernel with a VGA text-mode print driver (`src/impl/kernel/main.c`, `src/impl/x86_64/print.c`)
- Bootable ISO built with GRUB

## Build

The toolchain (cross-compiling GCC, NASM, GRUB) runs in Docker:

```bash
docker build buildenv -t myos-buildenv
docker run --rm -it -v "$(pwd)":/root/env myos-buildenv
make build-x86_64
```

The ISO is written to `dist/x86_64/kernel.iso`. Run it with QEMU:

```bash
qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso
```
