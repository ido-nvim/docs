# Event
The event loop of Ido. This is another module which you will rarely use, but is documented *just in case*

First of all load the event module

```lua
local event = require("ido.event")
```

## `event.async(ACTION)`
Execute the function `ACTION` separate from the main event loop of Neovim.

## `event.stop()`
Stop the event loop of Ido

## `event.exit()`
Exit out of Ido. This gets rid of the results, since ido has "exited" and there is nothing to accept

## `event.loop()`
The main loop of Ido. This function loops constantly while the `looping` [internal variable](main.md) is "truthy". It is essentially a *REPL*.

- It <ins>**R**</ins>eads the key presses using `getchar()`

- It <ins>**E**</ins>valuates the key presses by matching against the `keys` [option](config.md) and defaulting to `main.insert()`

- It <ins>**P**</ins>rints Ido in the echo area if needed

- It <ins>**L**</ins>oops while the afforementioned condition is true

## Advices?
There are no advices in this module. The event loop is something, I believe, which should *never* be customizable.
