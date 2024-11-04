---
date: 2022-08-02
showTableOfContents: true
slug: "projects"
title: "Projects"
type: "page"
image: "/images/codeberg.webp"
---

![Screenshot of my libre Git repositories, hosted on Codeberg.org](/images/codeberg.webp)

## Introduction

This is a portfolio of [my projects](https://codeberg.org/jamesericdavidson), presented in chronological order.

I provide comments on:

- What the project accomplishes
- When it was written
- How it functions
- And why it uses certain logic

Not all of my projects are discussed on this page. So stay tuned for more!

[The Summary is a stopgap until a Table of Contents is available for mobile.]: #

## Summary

Jump to the project which interests you the most.

[jimbOS](#jimbos)
: A custom Universal Blue image, derived from Fedora Silverblue

[jamesdavidson.xyz](#jamesdavidsonxyz)
: You are here!

[dotfiles](#dotfiles)
: Configuration files and scripts for Debian GNU/Linux systems

[Guild Wars 2 Pip Calculator](#guild-wars-2-pip-calculator)
: Estimate the time it will take complete divisions in the World vs World game mode

[Hire Car Maintenance Inc](#hire-car-maintenance-inc)
: A graphical user interface application for hire car companies

[Mastermind](#mastermind)
: A code-breaking game for two players

[Map Symbols](#map-symbols)
: Match the Ordnance Survey map symbol shown to the corresponding button

## jimbOS (2024) {#jimbos}

{{< figure src="/images/bluefin-autumn.webp" alt="Artwork of dinosaurs in a wooded forest. The image is tinted red to reflect autumn colours." attr="Image provided courtesy of the Universal Blue project." attrlink="https://universal-blue.discourse.group/t/dinosaur-gallery/18/4" >}}

### Synopsis

jimbOS employs a light-touch approach to customising the Linux desktop. It uses the [Bluefin](https://projectbluefin.io/) image provided by [Universal Blue](https://universal-blue.org/) as a base, and makes modifications as per my preferences.

The cloud native model afforded by Universal Blue sidesteps the issues of:

- Snowflake systems (a uniquely composed operating system which is difficult to replicate)
- Configuration management (a la Ansible playbooks)
- Package manager conflicts
- And so on...

Universal Blue is derived from [Fedora Silverblue](https://fedoraproject.org/atomic-desktops/silverblue/), and inherits the benefits of immutable and atomic systems (some of which are detailed in my '[openSUSE Aeon is the future of Linux](/posts/opensuse-aeon-is-the-future-of-linux/)' article).

jimbOS, Bluefin, and Universal Blue are licensed using the Apache License 2.0.

[View the source code](https://github.com/jamesericdavidson/jimbOS-bluefin-dx).

### Credits

I offer my thanks and congratulations to [Jorge Castro](https://www.ypsidanger.com/) and the [Universal Blue project](https://universal-blue.org/) for developing the infrastructure, images, documentation, and other tools responsible for enabling the cloud native model to thrive on desktop.

## jamesdavidson.xyz (2022-2024) {#jamesdavidsonxyz}

{{< figure src="/images/gokarna.webp" alt="An aerial photograph of Gokarna's Paradise Beach, taken during the daytime. Beachgoers and boats can be seen amongst rocks, trees, and sand." attr="Photo by [Raman Choudhary](https://unsplash.com/photos/aerial-view-of-people-on-beach-during-daytime-MyCKTYn9A78) on [Unsplash](https://unsplash.com)" >}}

### Synopsis

The project uses the [Hugo](https://gohugo.io/) static site generator.

The [Gokarna](https://github.com/gokarna-theme/gokarna-hugo) theme is licensed under the GNU General Public License v3.0.

Content is licensed under the Creative Commons Attribution-NoDerivatives 4.0 International License. With the exception of the [Linux Lab](/posts/the-linux-lab), which uses the GNU Free Documentation License, Version 1.3; with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.

[View the source code](https://codeberg.org/jamesericdavidson/jamesdavidson.xyz).

### Retrospective

#### Framework

I decided to use the Hugo framework for three reasons:

- To abstract away the design process
- Simplify content creation
- Adopt a mature platform (with good documentation)

A content management system such as WordPress is feature-rich, but complex. I don't need a graphical user interface or WYSIWYG editor, only a theme. The fewer dependencies and less code complexity, the better.

#### Theme

I settled on [Gokarna](https://github.com/gokarna-theme/gokarna-hugo), a theme which is minimal, responsive and themeable.

I'm now [a contributor to the project](https://github.com/gokarna-theme/gokarna-hugo/graphs/contributors), seeing pull requests merged upstream:

- [Improve copyright support](https://github.com/gokarna-theme/gokarna-hugo/pull/233)
- [Enhance documentation for first-time users](https://github.com/gokarna-theme/gokarna-hugo/pull/243)
- [Containerise screenshot script](https://github.com/gokarna-theme/gokarna-hugo/pull/262)
- [Link to the Next and Previous posts](https://github.com/gokarna-theme/gokarna-hugo/pull/124)
- [Support home page front matter](https://github.com/gokarna-theme/gokarna-hugo/pull/119)
- [Add front matter templates](https://github.com/gokarna-theme/gokarna-hugo/pull/241)
- ~~[Show the date a post was last modified](https://github.com/gokarna-theme/gokarna-hugo/pull/117)~~ This feature was approved [a year later](https://github.com/gokarna-theme/gokarna-hugo/pull/169) courtesy of another contributor.

### Credits

Thanks to [Yash Mehrotra](https://yashmehrotra.com/) and [Avijit Gupta](https://twitter.com/526avijit) for developing Gokarna, and [recognising my contributions](https://github.com/gokarna-theme/gokarna-hugo?tab=readme-ov-file#major-contributors) in the `README`.

## dotfiles (2018-2021) {#dotfiles}

{{< figure src="/images/tux-flat.webp" alt="Artwork depicting the Linux mascot, Tux" attr="Tux Flat is licensed under the GNU General Public License v2.0 or later." >}}

### Synopsis

dotfiles was the latest incarnation of my 'configuration files and scripts for Debian GNU/Linux systems'.

It was designed to accompany a network install of Debian with all `tasksel` items de-selected.

The project encompasses two years of development in 2020 and 2021, though prior incarnations were available in 2018 and 2019 respectively.

It is licensed using the GNU Public Licence version 3 only.

[View the source code](https://codeberg.org/jamesericdavidson/dotfiles).

### Retrospective

dotfiles was discontinued after I moved from Debian [to openSUSE Tumbleweed](/posts/security-in-opensuse-tumbleweed).

dotfiles was a moving target throughout development, as I changed tools, improved my understanding of the operating system, best practices within it, et cetera.

#### Branching

I learned to use three types of branches for dotfiles: main, development, and \<feature>.

- main
    
    Once a milestone had been met, and the files had been tested, a release would be tagged. The tag would then be pushed to main.

- development

    Add complete features (see below) and bug fixes as atomic commits, ensuring they are trivial to revert.

- \<feature>

    Features were merged into the development branch using the `--squash` option.

    In the past, I had experienced broken files after committing incomplete features to the development branch. This was problematic, as I lived on the development branch.

    Adopting feature branches largely cured this faux pas.

#### Code quality

I endeavoured to make files easy to understand, portable across machines, and use programmatic logic.

As a case study, I will refer to [this Polybar launch script](https://wiki.archlinux.org/index.php?title=Polybar&oldid=578417#Running_with_WM) from the ArchWiki.

The script performs a naive check to see if the `polybar` process has been killed:

```bash
# Terminate already running bar instances
killall -q polybar

# Wait until the processes have been shut down
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done
```

What does this script do, and how can it be improved?

* Perform a command to search for the string `polybar` amongst processes running on the system
    - Use a bash-specific variable to check that the process was launched by the current user
* If the command exits successfully (i.e. the process is still running), wait for one second before issuing the same command again
* When the command eventually fails, assume that this means the string was not found, and that `polybar` is no longer running

```bash
if pgrep --euid "$(id --user --name)" --exact polybar
then
    # Kill existing polybar processes
    killall --quiet polybar
    # Wait for the processes to die
    wait $!
fi
```

* Improve readability by using GNU long options
* Check the user id by using a POSIX-compliant command
* Programmatically wait for the previous command to finish executing

Using the `wait` built-in solves the problems present in the `do-while` loop. The `if` statement can be exited immediately, and there is no reliance on nebulous parsing of another program's output.

There are many reasons not to parse human-readable output to a script, for example if `pgrep`:

* Experiences API or ABI changes
* Is not installed on the system
* Has been modified by the distribution maintainer

### Credits

dotfiles was integral to my learning process for GNU/Linux.

I'm grateful to every single person who collaborated on the documentation I scoured to make dotfiles better.

## Guild Wars 2 Pip Calculator (2018) {#guild-wars-2-pip-calculator}

{{< figure src="/images/guild-wars-2.webp" alt="A screenshot of Guild Wars 2, depicting three player characters" attr="© 2021 NCSOFT Corporation. All rights reserved. NCSOFT, ArenaNet, the interlocking NC logo, Aion, Lineage II, Guild Wars, Guild Wars 2: Heart of Thorns, Guild Wars 2: Path of Fire, Blade & Soul, and all associated logos, designs, and composite marks are trademarks or registered trademarks of NCSOFT Corporation. All other trademarks are the property of their respective owners." attrlink="https://us.ncsoft.com/en-us/legal/ncsoft/content-terms-of-use" >}}

### Synopsis

For context, Guild Wars 2 is a Massively Multiplayer Online Roleplaying Game (MMORPG).

A reward system was introduced to the game, which awarded the player with 'pips' at five-minute intervals. The more pips a player receives per interval, the faster they can complete a reward tier.

In real-time, the calculator estimates how long it would take a player to complete reward tiers.

I was motivated to develop the tool as:

1. I wanted to use the functionality, and be able to share it with friends

    It turns out that doing these calculations manually is boring. Who knew?

2. A similar tool had not yet been publicly announced

    The project had its first commit in September 2018, though it was functional from an earlier date.

    Since that time, at least two comparable tools have been made available. See the [Guild Wars 2 Wiki](https://wiki.guildwars2.com/wiki/Special:RunQuery/WvW_skirmish_pip_query?) and [LimitlessFX](https://gw2.limitlessfx.com/wvw/pips.php).

Much like [Map Symbols](#map-symbols-synopsis), this project was written using HTML, CSS and JavaScript.

It is licensed using the Apache License 2.0.

[View the source code](https://codeberg.org/jamesericdavidson/pip-calculator).

### Demonstration

Try it, directly in the browser.

| [Calculate Pips](/demos/pip-calculator) |
| --------------------------------------- |
| ![Screenshot of the Pip Calculator](/images/pip-calculator-demo.webp "9 hours and 46 minutes? Ain't nobody got time for that!") |

### Retrospective

#### Appearance

Pip Calculator is functional, but not beautiful.

It is naively responsive, using the `viewport` meta tag, and `max-width` body property.

#### Functionality

The user enters a number of pips, optionally selects a tier to stop at, and is presented with the results.

Input is sanitised:

- `isNumberKey()`: The keys pressed must be between 0 and 9
- `isNumberAllowed()`: The value must be between 3 and 19

To ensure hours and minutes are displayed with or without plurals as appropriate, the `getCaseSwitch()` function is used to determine which strings should be used, using the values of `hours` and `minutes`.

#### Flaws

The total time given is not equal to the additive time of each tier.

Tiers are presented with floored hours and rounded minutes. However, the decimal values of each tier are retained when adding `timeToTier` to `totalTime`.

Only after every tier is calculated does `totalTime` have its hours floored and minutes rounded. This results in the total time being longer.

### Credits

After playing Guild Wars 2 for thousands of hours, I have something to show for it professionally. Thanks, ArenaNet!

## Hire Car Maintenance Inc (2017/18) {#hire-car-maintenance-inc}

{{< figure src="/images/avis.webp" alt="An Avis hire car parked on a road near water and snowy Norweigan mountains." attr="Photo by [Abhishek Umrao](https://unsplash.com/photos/PujiL9mZWNM) on [Unsplash](https://unsplash.com)" >}}

### Synopsis

Written in the 2017/18 academic year, using C# and .NET WinForms.

[View the source code](https://codeberg.org/jamesericdavidson/soft151-hire-car-maintenance-inc).

Hire Car Maintenance Inc serves as an introduction to object-oriented programming.

It is licensed using the Apache License 2.0.

### Retrospective

`input.txt` is parsed to create classes and objects at runtime. Changes made using the interface are saved persistently.

The interface was designed using Windows Forms Designer.

![Screenshot demonstration of Hire Car Maintenance Inc](/images/soft151-demo-1.webp)

As seen above, the user is able to:

- Search for companies and cars
- Add, remove or edit companies and cars

![Screenshot demonstration of the search bar functionality in Hire Car Maintenance Inc](/images/soft151-demo-2.webp)

### Credits

Once again, I had the pleasure of learning from Liz Stuart.

## Mastermind (2017/18) {#mastermind}

### Synopsis

Written in the 2017/18 academic year using C#. Compatible with .NET and Mono.

[View the source code](https://codeberg.org/jamesericdavidson/soft164-mastermind).

Mastermind is a code-breaking game for two players.

It is licensed using the Apache License 2.0.

### Retrospective

There were two stipulations for the design of this project:

- Write a console application, not a graphical user interface
- Avoid features of C# which are not available in C

![Screenshot demonstration of playing Mastermind](/images/mastermind-demo.webp)

The user defines the number of positions and colours, then plays against a randomly generated pattern.

The program is resilient to input errors, checking whether values are numeric and within bounds.

The code was developed under the scrutiny of the module leader, who defined what functionality was and was not acceptable. As a result, some C-specific code and quirks are used.

## Map Symbols (2016) {#map-symbols}

{{< figure src="/images/ordnance-survey-maps.webp" alt="Photograph depicting Ordnance Survey maps" attr="Photo by [Drew Collins](https://unsplash.com/photos/Nfgy5Jbbrf8) on [Unsplash](https://unsplash.com)" >}}

### Synopsis

My first project, written in the Autumn semester of the 2016/17 academic year. It employs HTML, CSS and JavaScript.

[View the source code](https://codeberg.org/jamesericdavidson/soft051-map-symbols/).

The goal of the game is to match the Ordnance Survey map symbol shown to the corresponding button.

It is licensed using the Apache License 2.0.

### Demonstration

Why not play from the browser and see for yourself?

| [Play Map Symbols](/demos/map-symbols) |
| ----------- |
| ![Screenshot demonstration of Map Symbols](/images/map-symbols-demo.webp) |

### Retrospective

To win the game, the user must have five correct answers on the scoreboard.

* The symbol shown must be pseudo-randomly generated

    The `Math.Random()` function is used to assign a number between `1` and `10` to `Num`, which is used to select a symbol from `imgArray`.

    To avoid a symbol being repeated immediately, the value of `Num` is assigned to `PreviousNum`. If the values in both variables are equal, `RandNum()` assigns a new number to `Num`, until `Num` and `PreviousNum` are no longer equal.

* A star must be "turned on" when a correct answer is given

    A new game begins with all five stars "turned off". The game is won when they are all "turned on".

    Each button fires an `onClick()` event to the `CheckAnswer()` function, which passes the `id` variable.

    The values of `id` and `Num` are compared:

    - If they are equal, the answer is correct
    - Else, the answer is incorrect

* A corresponding sound and message should be used whenever an answer is given

    Example of a correct answer:

    ![The message "Well done!" is displayed](/images/map-symbols-correct.webp)

    Example of an incorrect answer:

    ![The message "The correct answer is..." is displayed](/images/map-symbols-incorrect.webp)
    
    The sound functionality was provided by the deprecated `<bgsound>` element, but now uses the modern `<audio>` element to emulate the same behaviour.

### Credits

The respective module was taught by Mark Dixon and Liz Stuart, whose approach to teaching made learning to program a joy.
