# Delete
The string deleting code of Ido. It is defined in terms of the [motions](motions.md) module of Ido.

First of all load the delete module

```lua
local delete = require("ido.delete")
```

## Terminology
The advices and the function names all follow a similar pattern when it comes to this and the [cursor](cursor.md) module. Therefore you need to get used to some terminology used in this document, since it is pointless to document all the motions.

- `MOTION`: The motion applied when deleting

- `delete.MOTION()`: The function which selects the string described by `MOTION` and deletes it.

Advices:

- The advice wrapper ID is `execute@delete:MOTION`

- `MOTION`: Get rid of the motion string before or after the cursor to emulate the deletion

- `MOTION_results`: Fetch results after deleting the string

- `MOTION_impossible`: The deletion is impossible

For example:

- The `forward` motion, which moves forward a character

- The function which deletes a character forward is `delete.forward()`

- The function has the advice wrappers `execute@delete:forward`, `execute@delete:forward_render` and `execute@delete:forward_impossible`

## Motions
Every single motion defined in the `motions` module is used as a deletion movement.
