# Motions
The concept of motions is what separates Vim/NeoVim from other text editors. It is the primary force behind its composable nature which we all love. There are some motions or *nouns*, which we combine with actions or *verbs* to produce a result, a *phrase*. Ido is inspired by that concept. Of course, this does not benefit in the way you expect it to. Ido is a narrowing framework, a selection menu. It cannot and should not have the modes of Vim. The benefit this has on Ido is the reduced complexity of the code base. It makes it easy to define functions like cursor movement and deletions, without writing similar verbose code for each module, which defines the string it should work on.

Load the motions module
```lua
local motion = require("ido.motion")
```

Before you read this, this module by itself has no effect in the world, instead it is used as a library for creating the deletion and cursor positioning code which powers Ido.

## `motion.forward_possible()`
Checks if a forward motion of one character is possible or not.

Returns:
- `true` it is possible
- `false` it is not possible

## `motion.backward_possible()`
Checks if a backward motion of one character is possible or not.

Returns:
- `true` it is possible
- `false` it is not possible

## `motion.forward()`
Describes the motion to go forward a character. It can have two different return values depending on the context.

Returns:
- the string which is transposed from either sides of the cursor, and the side of the cursor it is transposed to (either `before` or `after`)
- `nil` in case this motion cannot be executed

## `motion.backward()`
Describes the motion to go backward a character.

Same kind of return value as above.

## `motion.forward_word()`
Describes the motion to go forward a word.

Same kind of return value as above.

## `motion.backward_word()`
Describes the motion to go backward a word.

Same kind of return value as above.

## `motion.line_start()`
Describes the motion to go to the beginning of the query text.

Same kind of return value as above.

## `motion.line_end()`
Describes the motion to go to the end of the query text.

Same kind of return value as above.
