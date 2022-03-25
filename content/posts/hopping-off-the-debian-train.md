---
title: "Hopping off the Debian train"
date: 2022-03-25T07:35:38Z
description: "Auf wiedersehen, pet"
type: "post"
---

# Gone with the wind

The sun has set on my [personalised Debian install](https://gitlab.com/jdxyz/dotfiles/-/tree/develop). Why?

The recent lapse in security updates to browser packages.

## Browser bungle

For a time, the Firefox and Chromium packages were susceptible to vulnerabilities already addressed upstream.

In both cases, out-of-date tooling was to blame. For Firefox, ensuring the package built on different architectures was a factor.

As a result, Debian elected to [discontinue Chromium security updates for Buster](https://www.debian.org/security/2022/dsa-5046), and [briefly removed the package from Bookworm](https://tracker.debian.org/news/1274273/chromium-removed-from-testing/).

For now, [Firefox](https://tracker.debian.org/pkg/firefox-esr) and [Chromium](https://tracker.debian.org/pkg/chromium) are being maintained again.

# Desktop security 

Debian's slovenly response to updating these packages made me think about the security of a desktop system.

## Display server

Current versions of [GNOME](https://wiki.gnome.org/Initiatives/Wayland/NVIDIA) and [KDE](https://community.kde.org/Plasma/Wayland/Nvidia) are capable of Wayland sessions on NVIDIA graphics cards.

X is [insecure](https://security.stackexchange.com/questions/4641/why-are-people-saying-that-the-x-window-system-is-not-secure/4646#4646) and [unwieldy](https://www.phoronix.com/scan.php?page=article&item=x_wayland_situation&num=1). Moving to a modern protocol is the only solution; nested X servers and sandboxing are unintuitive, and do not solve the fundamental design flaws of the server.

The issue of untrusted driver and firmware blobs remains, however.

## Sandboxed applications

As users, we trust that maintainers are packaging software within the ideals of the distribution. Ergo, [we may distrust software which isn't packaged by the maintainers](https://drewdevault.com/2021/09/27/Let-distros-do-their-job.html).

But if we have to stray outside of the repositories, how do we ensure the software behaves as expected, without risking other components of the system?

Perhaps with [Flatpak](https://docs.flatpak.org/en/latest/sandbox-permissions.html):

> One of Flatpak’s main goals is to increase the security of desktop systems by isolating applications from one another. This is achieved using sandboxing and means that, by default, applications that are run with Flatpak have extremely limited access to the host environment.

This approach is taken to the extreme by [Fedora Silverblue](https://docs.fedoraproject.org/en-US/fedora-silverblue/getting-started/), an immutable operating system which installs graphical applications from Flatpak.

# Release cadence

For the sake of simplicity, I argue that the paradigms for desktop and server use are mutually exclusive:

* If you are commissioning a server: choose a distribution with fixed, long-term support packages, that are updated throughout the distributions lifecycle, by the maintainers and upstream developers
* If you need a workstation: containerise your server operating system for testing, while using a rolling release distribution on the host

Given what I've discussed above, I've decided on openSUSE Tumbleweed. It is by no means a cure-all for the pitfalls of the Linux\* desktop, though [there are benefits](https://get.opensuse.org/tumbleweed/).

## Footnotes

1. User space today encompasses more than GNU; some distributions eschew GNU entirely. I choose to refer the operating system as Linux for the sake of consistency.
