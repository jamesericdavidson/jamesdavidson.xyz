---
date: 2023-04-02
description: "This post is immutable, I want you to read only"
showTableOfContents: true
slug: "opensuse-microos-desktop-is-the-future-of-linux"
tags: ["linux", "openSUSE", "immutable"]
title: "openSUSE MicroOS Desktop is the future of Linux"
type: "post"
---

# Introduction

openSUSE MicroOS Desktop provides the Chromebook experience, on Linux.

- Get all of your apps in one place
- Work without interruption, as updates occur in the background

# Paradigm

What advantages does this approach have?

{{< youtube id="vZ1LRe_foJY" title="The Cloud Native Linux Desktop Model" >}}

## Sandboxed

[Apps are isolated from each other](https://docs.flatpak.org/en/latest/basic-concepts.html), and the rest of the system.

You decide whether an app should be allowed to access your files, the internet, or your webcam.

## Immutable

Crucial files can't be modified while the system is running.

Instead, updates are applied the next time you start the computer.

## Rolling

Leverage the latest, thoroughly tested software (from openSUSE Tumbleweed).

Something not working properly? Roll the system back in time!

## Minimal

Get all the functionality you need, without having unnecessary software installed.

Ideal for computers with limited storage space.

## Containerised

[Run any Linux distribution](https://github.com/89luca89/distrobox) - any app, any service.

All seamlessly integrated into MicroOS.

# Apps

When installing apps, you will want to use [this order of preference](https://en.opensuse.org/Portal:MicroOS/Desktop#Ways_to_Install_Applications_in_Order_of_Preference):

1. Install device drivers with Transactional Update
2. Install graphical apps from GNOME Software
3. Install console apps using Distrobox

Most of the time, you'll be using GNOME Software.

## Transactional Update

Open the Terminal, and enter:

```
sudo transactional-update pkg install
```

Followed by the packages you want to install.

```
sudo transactional-update pkg install sl htop neofetch
```

These packages are used as an example. You should only install drivers for hardware that isn't supported out of the box.

You can search for packages on [the openSUSE website](https://software.opensuse.org/find), or [with `zypper`](https://en.opensuse.org/SDB:Zypper_usage#Searching_packages):

```
zypper search
```

### Pitfalls

Transactional updates are performed in the background, and will be cancelled if any errors are encountered during the update process.

For example, updating a package which requires a license agreement. With background updates, the user is unable to answer the prompt given by the package manager, causing the update to be cancelled.

## GNOME Software

> [Apps are isolated from each other, and the rest of the system.](#sandboxed)

Apps are confined to their own folder - this is beneficial, because there is no risk of breakage.

In a traditional Linux distribution, having two apps which rely on the same file can be risky. The file could be overwritten, or deleted.

In an immutable Linux distribution, these files are independent of each other, or shared in a read-only fashion.

### Permissions

> [You decide whether an app should be allowed to access your files, the internet, or your webcam.](#sandboxed)

Apps come with default permissions that you may not need.

If you are familiar with Linux concepts (such as display servers), read [this article about desktop Linux hardening](https://privsec.dev/posts/linux/desktop-linux-hardening/#flatpak), then [install Flatseal](https://flathub.org/apps/details/com.github.tchx84.Flatseal) to configure permissions.

Here are [some examples](https://codeberg.org/jamesericdavidson/flatpak-overrides) to get you started.

## Distrobox

> [Run any Linux distribution - any app, any service.](#containerised)

Distrobox is a powerful tool for users who aren't averse to using the terminal. Need an app that isn't available in GNOME Software? Install it from a Distrobox container instead.

On MicroOS, Distrobox defaults to installing an openSUSE Tumbleweed container. Packages on openSUSE are installed using the `zypper` command:

```
distrobox-enter
sudo zypper install neovim
```

Apps installed to a Distrobox container can be exported to MicroOS:

```
distrobox-enter
sudo zypper install neovim-gtk
distrobox-export --app nvim-gtk
```

The app will then appear in the list of applications:

{{< figure src="/images/neovim-gtk-on-distrobox.png" alt="Screenshot of the GNOME applications list - the search box contains the word 'neovim'" caption="Apps installed in a container are indistinguishable from apps installed with GNOME Software." >}}

### Exporting

The `--app` option requires the filename of the program. You can find this using `rpm`:

```
rpm --query --list neovim-gtk | grep /usr/bin
/usr/bin/nvim-gtk
```

`grep` is used to search for relevant results - programs are installed to the `/usr/bin` folder on openSUSE.

To learn more, type `distrobox-export --help`, or read the [source code comments](https://github.com/89luca89/distrobox/blob/main/distrobox-export).

# Conclusion

Suitable for both casual users and software developers, openSUSE MicroOS Desktop adopts the ChromeOS paradigm and transplants it to Linux with resounding success.

Do you enjoy the simplicity and security of installing apps from Google Play or the App Store? Then you'll love GNOME Software.

MicroOS Desktop is state of the art. Take notes, Windows and macOS.
