# Cursor
The cursor positioning code of Ido. It is defined in terms of the [motions](motions.md) module of Ido.

First of all load the cursor module

```lua
local cursor = require("ido.cursor")
```

## Terminology
The advices and the function names all follow a similar pattern when it comes to this and the [delete](delete.md) module. Therefore you need to get used to some terminology used in this document, since it is pointless to document all the motions.

- `MOTION`: The motion applied to the virtual cursor

- `cursor.MOTION()`: The function which executes the motion `MOTION`

Advices:

- The advice wrapper ID is `execute@cursor:MOTION`

- `MOTION`: Transpose the text before and after the cursor to emulate a cursor movement

- `MOTION_render`: Render Ido after transposing the text

- `MOTION_impossible`: The cursor movement is impossible

For example:

- The `forward` motion, which moves forward a character

- The function which moves the cursor is `cursor.forward()`

- The function has the advice wrappers `execute@cursor:forward`, `execute@cursor:forward_render` and `execute@cursor:forward_impossible`

## Motions
Every single motion defined in the `motions` module is used as a cursor movement.
