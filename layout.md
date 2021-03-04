# Layouts
A layout is a table of options which define the look and feel of Ido orientation-wise.

First of all load the layout module

```lua
local layout = require("ido.layout")
```

## Template
A layout consists of the following options:

| Options | Description |
| ------- | ----------- |
| `results_start` | The decoration before the results |
| `results_selected` | The decoration before the selected result |
| `results_separator` | The decoration which separates the results |
| `results_end` | The decoration after the results |
| `suggest_start` | The decoration before the suggestion |
| `suggest_end` | The decoration after the suggestion |
| `maximum_height` | The maximum height of the Ido interface |
| `dynamic_resize` | Dynamically change the height to the least value possible, constrained by `maximum_height` |
| `render_sequence` | The sequence in which layout "tokens" are rendered. See [examples](ex_layout.md) |

## `layout.new(OPTIONS)`
Create a new layout. It takes a table of options which describe the layout, and defaults to the template if some options are missing.

Returns:
- `nil` errors were encountered, along with this it will also print the error

- `true` success
