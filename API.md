# API

What is found in this document is guaranteed to be true in future, for all minor and patch version changes.

Breaking changes, where this document and the functioning of ```damned``` changes, will be indicated by a major version change.

---

## Essential Information

```damned``` does not parse the termcap file to see whether a method is available within your user's current terminal emulator. It will assume that if you call it, it can be done.

```damned``` traps the EXIT signal with a cleanup helper, ```damned_cleanup```. If you override that trap, make sure you call it on exit.


```damned``` traps the WINCH signal with the helper: ```damned_window_size```. If you override that trap, make sure you call it in your own signal handler.

```damned_*``` is reserved by ```damned```.

```damned``` is reserved by ```damned```.

```dWIDTH``` is reserved by ```damned```.

```dHEIGHT``` is reserved by ```damned```.

```dCURSOR_HEIGHT``` is reserved by ```damned```.

```dCURSOR_WIDTH``` is reserved by ```damned```.

---

## dWIDTH

This is a variable, that can be accessed and read by the user. (e.g. ```test "$dWIDTH" = '27';```)

It should reflect the current number of characters wide that the terminal is.

If a user changes this variable, it invokes undefined behaviour.

---

## dHEIGHT

This is a variable, that can be accessed and read by the user. (e.g. ```test "$dHEIGHT" = '27';```)

It should reflect the current number of characters high that the terminal is, also known as the number of lines.

If a user changes this variable, it invokes undefined behaviour.

---

## dCURSOR_WIDTH

This is a variable, that can be accessed and read by the user. (e.g. ```test "$dCURSOR_WIDTH" = '27';```)

It should reflect the current number of characters across that the cursor currently is, or the line position of the cursor.

If a user changes this variable, it invokes undefined behaviour.


---

## dCURSOR_HEIGHT

This is a variable, that can be accessed and read by the user. (e.g. ```test "$dCURSOR_HEIGHT" = '27';```)

It should reflect the current number of characters high that the cursor currently is, or the line number that the cursor is on.

If a user changes this variable, it invokes undefined behaviour.

---

## damned_cleanup

This function is usually called by the EXIT signal, unless you override it.

It attempt to restore the terminal back to it's initial state.

---

## damned_window_size

This function is usually called by the WINCH signal, unless you override it.

It attempts to update the above variables to the correct values.

---

## damned

This is the main function, that it is expected you will use.

As it takes a sequence of arguments, you can supply them using variables, if you decide to structure your program that way.

### damned echo

```damned echo``` takes one argument, of either ```disable``` or ```enable```.

* ```damned echo disable``` turns automatic echoing off on the terminal.
* ```damned echo enable``` restores the normal behaviour.

### damned term

```damned term``` takes one argument, of either ```uncook``` or ```restore```.

* ```damned term uncook``` turns off buffering on the terminal.
* ```damned term restore``` restores the terminal to it's initial state.

Note: There is *no* ```cook```. Full restoration of the terminal is your only option.

### damned cursor

```damned cursor``` allows you to interact with the user's cursor on the terminal.

* ```damned cursor refresh``` will update the ```dCURSOR_HEIGHT``` and ```dCURSOR_WIDTH``` values. This is not done automatically, because it is an expensive operation of at least 200ms, which involves redirecting the tty temporarily.
* ```damned cursor up``` Moves the user's cursor up one line. Behaviour is undefined if the cursor is at the limit.
* ```damned cursor down``` Moves the user's cursor down one line. Behaviour is undefined if the cursor is at the limit.
* ```damned cursor left``` Moves the user's cursor to the left one character. Behaviour is undefined if the cursor is at the limit.
* ```damned cursor right``` Moves the user's cursor to the right one character. Behaviour is undefined if the cursor is at the limit.
* ```damned cursor save``` Saves the current cursor position.
* ```damned cursor restore``` Moves the cursor to the last saved cursor position. Behaviour is undefined if no save had taken place.

### damned clear

```damned clear``` allows you to clear various parts of the screen.

* ```damned clear screen``` clears the entire screen.
* ```damned clear screen before``` clears the portion of the screen immediately before the cursor.
* ```damned clear screen after``` clears the portion of the screen immediately following the cursor.
* ```damned clear line``` clears the entirety of the line the cursor is on.
* ```damned clear line before``` clears the portion of the line immediately before the cursor.
* ```damned clear line after``` clears the portion of the line immediately following the cursor.

## damned effect

```damned effect``` applies or removes various text effects present on the terminal.

* ```damned effect bold``` enables bold text on the terminal.
* ```damned effect underline``` enables underline text on the terminal.
* ```damned effect blink``` enables blinking text on the terminal.
* ```damned effect reverse``` enables reversed text on the terminal.
* ```damned effect invisible``` enables invisible text on the terminal.
* ```damned effect reset``` removes all active effects or colourings on the terminal.

## damned fg

```damned fg``` changes foreground colourings, or text colourings, on the terminal.

* ```damned fg 256``` takes an argument of 0-256, and uses that to colour the text.
* ```damned fg true``` takes three arguments of 0-256. The first represents a percentage of red, the second a percentage of green, and the third a percentage of blue. The RGB value is used to colour the text.
* ```damned fg black``` sets the text to basic black colouring.
* ```damned fg red``` sets the text to basic red colouring.
* ```damned fg green``` sets the text to basic green colouring.
* ```damned fg yellow``` sets the text to basic yellow colouring.
* ```damned fg blue``` sets the text to basic blue colouring.
* ```damned fg magenta``` sets the text to basic magenta colouring.
* ```damned fg cyan``` sets the text to basic cyan colouring.
* ```damned fg white``` sets the text to basic white colouring.
* ```damned fg bright-black``` sets the text to black colouring.
* ```damned fg bright-red``` sets the text to red colouring.
* ```damned fg bright-green``` sets the text to green colouring.
* ```damned fg bright-yellow``` sets the text to yellow colouring.
* ```damned fg bright-blue``` sets the text to blue colouring.
* ```damned fg bright-magenta``` sets the text to magenta colouring.
* ```damned fg bright-cyan``` sets the text to cyan colouring.
* ```damned fg bright-white``` sets the text to white colouring.

## damned bg

```damned bg``` changes background colourings, on the terminal.

* ```damned bg 256``` takes an argument of 0-256, and uses that to colour the background.
* ```damned bg true``` takes three arguments of 0-256. The first represents a percentage of red, the second a percentage of green, and the third a percentage of blue. The RGB value is used to colour the background.
* ```damned bg black``` sets the background to basic black colouring.
* ```damned bg red``` sets the background to basic red colouring.
* ```damned bg green``` sets the background to basic green colouring.
* ```damned bg yellow``` sets the background to basic yellow colouring.
* ```damned bg blue``` sets the background to basic blue colouring.
* ```damned bg magenta``` sets the background to basic magenta colouring.
* ```damned bg cyan``` sets the background to basic cyan colouring.
* ```damned bg white``` sets the background to basic white colouring.
* ```damned bg bright-black``` sets the background to black colouring.
* ```damned bg bright-red``` sets the background to red colouring.
* ```damned bg bright-green``` sets the background to green colouring.
* ```damned bg bright-yellow``` sets the background to yellow colouring.
* ```damned bg bright-blue``` sets the background to blue colouring.
* ```damned bg bright-magenta``` sets the background to magenta colouring.
* ```damned bg bright-cyan``` sets the background to cyan colouring.
* ```damned bg bright-white``` sets the background to white colouring.