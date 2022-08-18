---
lastmod: 2022-08-12
title: "How to internally flash Libreboot on a ThinkPad"
type: "post"
date: 2022-08-08
showTableOfContents: true
description: "Give me liberty, or give me RISC-V!"
tags: ["linux", "privacy", "cybersecurity", "tutorial"]
weight: 25
---

# Introduction

The Libreboot documentation can be confusing to navigate and understand.

This is a guide on how to internally flash Libreboot, on [GM45 ThinkPads](https://libreboot.org/docs/hardware/#laptops-intel-x86) which have already had their BIOS flashed externally.

# Quick setup

- Install `flashrom` and `ich9gen` (found here: [`ich9utils`](https://notabug.org/libreboot/ich9utils)[^ich9])
    - `ich9utils` must be compiled, using `make` and `gcc`

[^ich9]: `flashrom` may be available from distribution repositories (due to its role in upstream coreboot), but `ich9utils` was developed exclusively for [GM45 machines](https://libreboot.org/docs/install/#howto-readwriteerase-the-boot-flash-please-check-list-of-exceptions-below-before-you-attempt-this), and is therefore available from the Libreboot project.

- [Download the latest Libreboot release](https://libreboot.org/download.html#https)
- On the target machine, [generate a `.bin` file containing the MAC address of the ethernet interface](https://libreboot.org/docs/install/ich9utils.html#ich9gen)[^eth]

[^eth]: Be aware of the differences between the traditional `eth0` interface, and [Predictable Network Interface Names](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/) in `systemd`.

```sh
# Determine the MAC address of the ethernet interface
ip link
# Enter the MAC address
ich9gen --macaddress 00:1f:16:80:80:80
```

- Write the `.bin` file to the Libreboot ROM, [noting the size of the flash chip](https://libreboot.org/docs/install/#flash-chip-size)
    - [`flashrom` will throw an error unless the kernel parameter `iomem=relaxed` is set](https://www.flashrom.org/FAQ#What_can_I_do_about_/dev/mem_errors?)

```sh
# Note the size of the flash chip, and write the appropriate .bin
# 4m, 8m or 16m
flashrom -p internal
# Write the .bin to the ROM
dd if=ich9fdgbe_8m.bin of=libreboot.rom bs=12k count=1 conv=notrunc
```

- [Write the ROM to the flash chip](https://libreboot.org/docs/install/#howto-readwriteerase-the-boot-flash-please-check-list-of-exceptions-below-before-you-attempt-this)
    - The flash chip must be specified using the `-c` option

```sh
sudo flashrom -p internal:laptop=force_I_want_a_brick,boardmismatch=force -w libreboot.rom
```

- Dump the flashed ROM and compare the hashes

```sh
# Make multiple dumps from the chip
sudo flashrom -p internal:laptop=force_I_want_a_brick,boardmismatch=force -r dump1.bin
sudo flashrom -p internal:laptop=force_I_want_a_brick,boardmismatch=force -r dump2.bin
sudo flashrom -p internal:laptop=force_I_want_a_brick,boardmismatch=force -r dump3.bin
# Compare the hashes against the ROM, ensuring that they are all the same
sha1sum dump*.bin libreboot.rom
```

And done.
