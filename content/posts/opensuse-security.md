---
title: "Security in openSUSE Tumbleweed"
tags: ["opensuse", "linux", "cybersecurity"]
date: 2022-05-24
description: "What you can expect after booting the installation media"
type: "post"
weight: 20
showTableOfContents: true
---

[This page is licensed under a Creative Commons Attribution-NoDerivatives 4.0 International License.]: # 

# Introduction {#introduction}

Note that this article is about Tumbleweed on the desktop - not Leap, MicroOS or Kubic.

For most users, everything you need is configured during installation, and manually in YasT.

# Installer {#installer}

The Tumbleweed installer is the best I've seen, security features notwithstanding. This praise extends to GeckoLinux, [an openSUSE spin](https://geckolinux.github.io/#how-different).

Out of the box, it can configure Secure Boot and encrypted swap. Moreover, Secure Boot *works*.

AppArmor, microcode and firewalld are included too. Though AppArmor has few profiles, and firewalld is not installed by default on GeckoLinux.

# YasT {#yast}

Works as intended, with a couple of pitfalls.

## Pitfalls {#pitfalls}

1. Flatpak throws `fusermount` errors with secure file permissions

Continue using the default easy profile, which is acceptable for ['typical single user desktop systems'](https://en.opensuse.org/openSUSE:Security_Documentation#Available_Profiles).

2. Disabling `systemd-remount-fs.service` leaves the root filesystem in read-only mode

YasT flags this as an extra service which 'is a potential target of a security attack'.

The service doesn't like to be disabled, and you might be tempted to `systemctl mask` it... don't do that. `zypper` will complain:

> The target filesystem is mounted as read-only. Please make sure the target filesystem is writeable.

Leave the service enabled.

## Recommendations {#recommendations}

Make these changes to maximise the benefits of the features configured by the installer:

* Disable Magic SysRq Keys
* Auto + [No SMT](https://www.privacyguides.org/linux-desktop/hardening/#simultaneous-multithreading-smt) CPU Mitigations
* Protect Boot Loader with Password
	* Protect Entry Modification Only

Note that the GRUB user is `root`.

In tandem, you should password protect the BIOS/UEFI to [prevent an attacker from disabling Secure Boot](https://www.privacyguides.org/linux-desktop/hardening/#secure-boot).

### GeckoLinux {#geckolinux}

* [Remove `/etc/gdm/custom.conf` to start the Wayland session](https://github.com/geckolinux/geckolinux-project/issues/191#issuecomment-772202462)

# Conclusion {#conclusion}

Tumbleweed ticks all the boxes, to name a few:

* Easy to install, use and maintain
* Packages in-step with upstream
* Snapshot rollbacks

Not covered above, but you should make use of Wayland and LUKS for more security and privacy.

That's all for now, bye!
