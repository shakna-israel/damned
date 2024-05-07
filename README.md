# damned

## curses for the shell

---

* [FAQ](#frequently-asked-questions)
  * [Shell...?](#shell)
  * [What!?](#what)
  * [Does it implement curses API?](#does-it-implement-curses-api)
  * [Hey! This doesn't behave the same way curses does!](#hey-this-doesnt-behave-the-same-way-curses-does)
  * [Will you implement a feature for me?](#will-you-implement-a-feature-for-me)
  * [Why won't you accept my pull request?](#why-wont-you-accept-my-pull-request)
  * [I find your tone impolite.](#i-find-your-tone-impolite)
* [Usage](#usage)
* [LICENSE](#license)

---

## Frequently Asked Questions

### Shell...?

Unfortunately, this requires a few bash-isms. I'd like to get rid of them, but at the moment, it does require something that implements the Bash interface, such as bash, zsh, etc.

Dash and others won't work.

### What!?

Well, it's been done before. Like [Shell Curses](https://www.ibm.com/developerworks/aix/library/au-shellcurses/index.html), implemented in ksh.

Partly, I've made this because I can.

Partly because I now know far more about ANSI escapes than I want.

Partly to show that every CLI-manipulation question doesn't need to be answered with 'use curses'.

### Does it implement curses API?

No. I don't feel like gouging my eyes out when writing my own documentation.

That and that Object-Oriented isn't a good fit for shell.

### Hey! This doesn't behave the same way curses does!

No. Because curses feels the need to do things that aren't actually necessary, like clearing the console when creating a new window.

You may want to, but you may manage your program another way. Why should the API get in the way of that?

### Will you implement a feature for me?

*shrug*. Maybe.

If you ask nicely. (Or pay me. Either is accepted.)

And if I have the time.

And if I can find a way too.

### Why won't you accept my pull request?

I'm sorry. I really want to.

Unfortunately, somebody decided copyright needed to be incredibly complicated.

So, when I turned around and decided that ```damned``` should be Public Domain, I found I *can't* even make my own work Public Domain.

I can use the Creative Commons 0 License, which I have, but that would mean everyone who contributes would have to do the same... And I can't assess whether or not that is actually legally binding in any way.

Please, *please*, go yell at your government about it. Mine too.

### I find your tone impolite.

I have found that my background and culture rubs American and Asian folks up the wrong way. I'm sorry, I'm an Australian. I lived in a place that used 'C U in the NT' as their international tourism slogan.

---

## Usage

```
# Load the framework, assuming it is in the same folder
. ./damned

# Access via the damned function...
damned fg red
echo 'This is red!'
damned bg blue
echo 'This is red text on a blue background!'
sleep 2s
damned clear screen
damned term uncook
damned echo disable
key=$(damned getch)
if [ "$key" = '119' ]; then
  damned cursor up
fi
```

Things you need to know:

* ```damned``` does not parse the termcap file to see whether a method is available within your user's current terminal emulator. It will assume that if you call it, it can be done.
* ```damned``` traps the EXIT signal with a cleanup helper, ```damned_cleanup```. If you override that trap, make sure you call it on exit.
* ```damned``` traps the WINCH signal with the helper: ```damned_window_size```. If you override that trap, make sure you call it in your own signal handler.
* ```damned_*``` is reserved by ```damned```.
* ```damned``` is reserved by ```damned```.

The exact functions and variables made available by the framework for the user is in the [API.md](API.md) document.

---

## LICENSE

Creative Commons 0 License.

As close to Public Domain as I can.

See [LICENSE](LICENSE) for the exact legal code, and ramifications for you, which should mostly be relief, not irritation.
