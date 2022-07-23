---
title: "Software Projects"
type: "page"
showTableOfContents: true
date: 2022-07-16
---

This is a portfolio of my noteworthy software projects.

I provide comments on what the project is, when it was written, how and why it uses certain logic.

All of the projects below are [available on GitLab](https://gitlab.com/jamesericdavidson).

# Personal projects {#personal-projects}

## dotfiles {#dotfiles}

### Synopsis {#dotfiles-synopsis}

dotfiles was the latest incarnation of my 'configuration files and scripts for Debian GNU/Linux systems'.

It was designed to accompany a network install of Debian with all `tasksel` items de-selected.

The project encompasses two years of development in 2020 and 2021, though prior incarnations were available in 2018 and 2019 respectively.

It is licensed using the GNU Public Licence version 3 only.

[View the source code](https://gitlab.com/jamesericdavidson/dotfiles).

### Retrospective {#dotfiles-retrospective}

dotfiles was discontinued after I moved from Debian [to openSUSE Tumbleweed](/posts/opensuse-security).

dotfiles was a moving target throughout development, as I changed tools, improved my understanding of the operating system, best practices within it, et cetera.

#### Branching {#dotfiles-retrospective-branching}

I learned to use three types of branches for dotfiles: main, development, and \<feature>.

- main
    
    Once a milestone had been met, and the files had been tested, a release would be tagged. The tag would then be pushed to main.

- development

    Add complete features (see below) and bug fixes as atomic commits, ensuring they are trivial to revert.

- \<feature>

    Features were merged into the development branch using the `--squash` option.

    In the past, I had experienced broken files after committing incomplete features to the development branch. This was problematic, as I lived on the development branch.

    Adopting feature branches largely cured this error in judgement.

#### Code quality {#dotfiles-retrospective-code-quality}

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

### Credits {#dotfiles-credits}

dotfiles was integral to my learning process for GNU/Linux.

I'm grateful to every single person who collaborated on the documentation I scoured to make dotfiles better.

## Guild Wars 2 Pip Calculator {#guild-wars-2-pip-calculator}

![A screenshot of Guild Wars 2, depicting three players in the World versus World game mode](/images/guild-wars-2.jpg "This is how cool you can look when you have no life! I would know, my character looks like this.")

### Synopsis {#guild-wars-2-pip-calculator-synopsis}

For context, Guild Wars 2 is a Massively Multiplayer Online Roleplaying Game (MMORPG).

A reward system was introduced into the game, which awarded player "pips" at five minutes intervals. The more pips a player receives, the faster they chip away at the total number of pips required to complete a tier.

The calculator estimates how long it would take a player to receive the rewards given upon the completion of a tier.

I was motivated to develop the tool as:

1. I wanted to use the functionality, and be able to share it with my friends

    It turns out that doing these calculations manually is boring. Who knew?

2. A similar tool had not yet been publicly announced

    Since that time, at least two comparable tools are available. See the [Guild Wars 2 Wiki](https://wiki.guildwars2.com/wiki/Special:RunQuery/WvW_skirmish_pip_query?) and [LimitlessFX](https://gw2.limitlessfx.com/wvw/pips.php).

Much like [Map Symbols](#map-symbols-synopsis), this project was written using HTML, CSS and JavaScript.

It is licensed using the Apache License 2.0.

[View the source code](https://gitlab.com/jamesericdavidson/pip-calculator).

### Demonstration {#guild-wars-2-pip-calculator-demonstration}

Try it, directly in the browser.

| [Calculate Pips](/demos/pip-calculator) |
| --------------------------------------- |
| [![Screenshot of the Pip Calculator](/images/pip-calculator-demo.png "9 hours and 46 minutes? Ain't nobody got time for that!")](/demos/pip-calculator) |

### Retrospective {#guild-wars-2-pip-calculator-retrospective}

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

### Credits {#guild-wars-2-pip-calculator-credits}

Thanks [ArenaNet](https://www.guildwars2.com/en/media/screenshots/) and [NCSoft](#copyright-notices-ncsoft-corporation) for use of the [above screenshot](#guild-wars-2-pip-calculator).

After playing Guild Wars 2 for thousands of hours, I have something to show for it professionally. Thanks again, ArenaNet!

# University projects {#university-projects}

Most of my University projects are licensed using the Apache License 2.0, as [recommended by the GNU Project](https://www.gnu.org/licenses/license-recommendations.html#small).

## Map Symbols {#map-symbols}

### Synopsis {#map-symbols-synopsis}

My first project, written in the Autumn semester of the 2016/17 academic year. It employs HTML, CSS and JavaScript.

[View the source code](https://gitlab.com/jamesericdavidson/soft051-map-symbols/-/blob/main/Game.html).

The goal of the game is to match the Ordnance Survey map symbol shown to the corresponding button.

### Demonstration {#map-symbols-demonstration}

Why not play from the browser and see for yourself?

| [Play Map Symbols](/demos/map-symbols) |
| ----------- |
| [![Screenshot of Map Symbols](/images/map-symbols-demo.png)](/demos/map-symbols) |

### Retrospective {#map-symbols-retrospective}

To win the game, the user must have five correct answers on the scoreboard.

* The symbol shown must be pseudo-randomly generated

    The `Math.Random()` function is used to assign a number between `1` and `10` to `Num`, which is used to select a symbol from `imgArray`.

    To avoid a symbol being repeated immediately, the value of `Num` is assigned to `PreviousNum`. If the values in both variables are equal, `RandNum()` assigns a new number to `Num`, until `Num` and `PreviousNum` are no longer equal.

* A star must be "turned on" when a correct answer is given

    A new game begin with all five stars "turned off". The game is won when they are all "turned on".

    Each button fires an `onClick()` event to the `CheckAnswer()` function, which passes the `id` variable.

    The values of `id` and `Num` are compared:

    - If they are equal, the answer is correct
    - Else, the answer is incorrect

* A corresponding sound and message should be used whenever an answer is given

    Example of a correct answer:

    ![The message "Well done!" is displayed](/images/map-symbols-correct.png)

    Example of an incorrect answer:

    ![The message "The correct answer is..." is displayed](/images/map-symbols-incorrect.png)
    
    The sound functionality was provided by the deprecated `<bgsound>` element, but now uses the modern `<audio>` element to emulate the same behaviour.

### Credits {#map-symbols-credits}

The respective module was taught by Mark Dixon and Liz Stuart, whose approach to teaching made learning to program a joy.

# More projects coming soon...

I'm gradually making more projects public on GitLab!

# Copyright Notices {#copyright-notices}

## James Davidson {#copyright-notices-james-davidson}

This work is licensed under a [Creative Commons Attribution-NoDerivatives 4.0 International License](http://creativecommons.org/licenses/by-nd/4.0/).

## NCSOFT Corporation {#copyright-notices-ncsoft-corporation}

<https://us.ncsoft.com/en-us/legal/ncsoft/content-terms-of-use>

© 2021 NCSOFT Corporation. All rights reserved. NCSOFT, ArenaNet, the interlocking NC logo, Aion, Lineage II, Guild Wars, Guild Wars 2: Heart of Thorns, Guild Wars 2: Path of Fire, Blade & Soul, and all associated logos, designs, and composite marks are trademarks or registered trademarks of NCSOFT Corporation. All other trademarks are the property of their respective owners. 
