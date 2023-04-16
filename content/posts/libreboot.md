---
aliases:
    - "/posts/libreboot-internal-flash/"
date: 2022-08-08
description: "Give me liberty, or give me RISC-V!"
lastmod: 2023-04-16
showTableOfContents: true
slug: "how-to-internally-flash-libreboot-on-a-thinkpad"
tags: ["linux", "privacy", "cybersecurity", "tutorial"]
title: "How to internally flash Libreboot on a ThinkPad"
type: "post"
---

# Introduction

The Libreboot documentation can be difficult to understand, and even more confusing to navigate.

This is a guide on how to internally flash Libreboot, on [GM45 ThinkPads](https://libreboot.org/docs/hardware/#laptops-intel-x86) which have already had their BIOS flashed externally.

# Quick setup

- Install `flashrom` and `ich9gen` (found here: [`ich9utils`](https://notabug.org/libreboot/ich9utils) [^ich9])
    - `ich9utils` must be compiled, using `make` and `gcc`

[^ich9]: `flashrom` may be available from distribution repositories (due to its role in upstream coreboot), but `ich9utils` was developed exclusively for [GM45 machines](https://libreboot.org/docs/install/#howto-readwriteerase-the-boot-flash-please-check-list-of-exceptions-below-before-you-attempt-this), and is therefore only available from the Libreboot project.

- [Download the latest Libreboot release](https://libreboot.org/download.html#https)
- On the target machine, [generate a `.bin` file containing the MAC address of the ethernet interface](https://libreboot.org/docs/install/ich9utils.html#ich9gen) [^eth]

    ```sh
    # Determine the MAC address of the ethernet interface
    ip link
    # Enter the MAC address
    ich9gen --macaddress 00:1f:16:80:80:80
    ```

[^eth]: Be aware of the differences between the traditional `eth0` interface, and [Predictable Network Interface Names](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/) in `systemd`.

- Write the `.bin` file to the Libreboot ROM, [noting the size of the flash chip](https://libreboot.org/docs/install/#flash-chip-size)
    
    - [`flashrom` throws `/dev/mem` errors, unless the `lpc_ich` kernel module is removed](https://www.flashrom.org/FAQ#What_can_I_do_about_/dev/mem_errors?)

        ```sh
        sudo modprobe -r lpc_ich
        ```

    ```sh
    # Note the size of the flash chip, and write the appropriate .bin
    # 4m, 8m or 16m
    flashrom -p internal

    # Write the .bin to the ROM
    dd if=ich9fdgbe_8m.bin of=libreboot.rom bs=12k count=1 conv=notrunc
    ```

- [Write the ROM to the flash chip](https://libreboot.org/docs/install/#howto-readwriteerase-the-boot-flash-please-check-list-of-exceptions-below-before-you-attempt-this)
    - In addition, the flash chip must be specified using the `-c` option

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
