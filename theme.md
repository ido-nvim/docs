# Themes
The module which decides the aesthetics of Ido. The following message is to the ricers: *Ready. Set. Go!*

Load it

```lua
local theme = require("ido.theme")
```

## Template
A template theme

| UX Elememt | Description |
| ---------- | ----------- |
| `prompt` | The prompt |
| `normal` | The normal highlight color |
| `cursor` | The virtual cursor |
| `ux` | The UX elements as defined in the [layout](layout.md) |
| `selected` | The selected result |
| `suggestion` | The suggestion text |

## Options
This module is just there so don't have to write `VimL` for configuring Ido, because quite frankly, it sucks.

The way you supply the color properties to the theme is the exact same way you supply them to the `:highlight` command in Vim. Here's a small example:

```lua
cursor = {
   guifg = "#161616",
   guibg = "#cc8c3c",
   gui = "bold"
}
```

And here's another:
```lua
ux = {
   link = "Special"
}
```

This will link to `Normal`:
```lua
normal = {}
```

## `theme.new(OPTIONS)`
Create a new theme. It automatically defaults to the template theme.

Params:
- `OPTIONS` The options which specify the theme. See the [examples](ex_theme.md)

Returns:
- `nil` if errors were encountered, in which case it will print them

- `true` success
