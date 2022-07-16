---
title: "Software Projects"
type: "page"
showTableOfContents: true
date: 2022-07-16
---

This is a portfolio of my software projects, including links, screenshots and comments about them.

Most of my University projects are licensed using the Apache License 2.0, as [recommended by the GNU Project](https://www.gnu.org/licenses/license-recommendations.html#small).

# Map Symbols

My first project, written in the Autumn semester of the 2016/17 academic year. It employs HTML, CSS and JavaScript.

The respective module was taught by Mark Dixon and Liz Stuart, whose approach to teaching made learning to program a joy.

[View the source code here](https://gitlab.com/jamesericdavidson/soft051-map-symbols/-/blob/main/Game.html).

## How it works

The goal of the game is to match the Ordnance Survey map symbol shown to the corresponding button.

To win the game, the user must have five correct answers on the scoreboard.

* The symbol shown must be psuedo-randomly generated 

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

    ![The message "Well done!" is displayed](/images/soft051-correct.png)

    Example of an incorrect answer:

    ![The message "The correct answer is..." is displayed](/images/soft051-incorrect.png)
    
    The sound functionality was provided by the deprecated `<bgsound>` element, but now uses the modern `<audio>` element to emulate the same behaviour.

# More projects coming soon...

I'm gradually making more projects public on GitLab!

*Next up: [Mastermind](https://gitlab.com/jamesericdavidson/soft164-mastermind)*.

---

This work is licensed under a [Creative Commons Attribution-NoDerivatives 4.0 International License](http://creativecommons.org/licenses/by-nd/4.0/).
