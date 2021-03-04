# Renderer
The part of Ido which does all the rendering. This is another module which you will rarely ever use

First of all load the module
```lua
local render = require("ido.render")
```

## `render.draw()`
Draw Ido in the echo area. It just calls `:redraw` and then executes the buffered command which brings the interface of Ido into existence.

## `render.queue()`
Queues a string to be drawn once it is required.

Params:
- `string` The string to draw

- `highlight` The highlight color of the string, defaults to `ido_normal`

- `force` Whether it should draw the text right away instead of buffering it, defaults to `false`

Returns:
- `true` if more strings can be rendered

- `false` if the previous condition is false

## `render.tokens.prompt()`
Draw the prompt

Returns:
- Same as above

## `render.tokens.query()`
Draw the query and the suggestion

Returns:
- Same as above

## `render.tokens.results()`
Draw the results

Returns:
- Same as above

## `render.start()`
Start the rendering

Returns:
- `true`
