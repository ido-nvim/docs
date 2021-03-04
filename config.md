# Configuration
Basic configuration system. Use this to change the options of Ido in a user-friendly and *syntax-sugary* way.

First of all, load the configuration api.

```lua
local config = require("ido.config")
```

## Concept
In Ido there are some options which you can change in order to change its behaviour. Without going into ![details](options_variables.md), when using the configuration api, it will set the fallback values for Ido. All the options discussed below are changeable by the `ido.start()` function. This exists as a way to automatically fallback to some default settings, in case the options are not provided in the start function.

## Options
| Option | Description | Defaults |
| ------ | ----------- | -------- |
| `prompt` | The prompt before the query | `">>> "` |
| `layout` | The name of the [layout](layout.md) | `"default"` |
| `theme` | The name of the [theme](theme.md) | `"default"` |
| `case_sensitive` | Match items case sensitively | `false` |
| `fuzzy_matching` | Match items fuzzily | `true` |
| `word_separators` | Sequence of characters which mark the word boundaries | `"|/?,.;: "` |

There is also another option: `keys`. It is the table of key mappings used in Ido.
```lua
keys = {

   ["<Right>"] = "ido.cursor.forward",
   ["<Left>"] = "ido.cursor.backward",

   ["<C-f>"] = "ido.cursor.forward",
   ["<C-b>"] = "ido.cursor.backward",

   ["<C-Right>"] = "ido.cursor.forward_word",
   ["<C-Left>"] = "ido.cursor.backward_word",

   ["<M-f>"] = "ido.cursor.forward_word",
   ["<M-b>"] = "ido.cursor.backward_word",

   ["<C-a>"] = "ido.cursor.line_start",
   ["<C-e>"] = "ido.cursor.line_end",

   ["<C-n>"] = "ido.result.next",
   ["<C-p>"] = "ido.result.prev",

   ["<Down>"] = "ido.result.next",
   ["<Up>"] = "ido.result.prev",

   ["<BS>"] = "ido.delete.backward",
   ["<Del>"] = "ido.delete.forward",

   ["<C-k>"] = "ido.delete.backward",
   ["<C-d>"] = "ido.delete.forward",

   ["<C-BS>"] = "ido.delete.backward_word",
   ["<C-Del>"] = "ido.delete.forward_word",

   ["<M-k>"] = "ido.delete.backward_word",
   ["<M-d>"] = "ido.delete.forward_word",

   ["<C-w>"] = "ido.delete.line_start",
   ["<M-w>"] = "ido.delete.line_end",

   ["<Tab>"] = "ido.accept.suggestion",
   ["<CR>"] = "ido.accept.selected",
   ["<Esc>"] = "ido.event.exit"
}
```

## `config.set(OPTIONS)`
The interface to the configuration api of Ido. It sets the options, that's all it does.

It takes a table of options as an argument, where the keys act as the option name, and the values as the final value to be set. It does a recursive extend via `vim.tbl_deep_extend()`, so the following code snippet will not overwrite the entire keys definition. It will merely add the keys present in the table to the keys table in the default options.

```lua
config.set{
   keys = {
      ["<C-b>"] = "ido.cursor.forward_word"
   },

   prompt = "Match: "
}
```

Returns:
- `true`

## Key mappings
How does the `keys` option work? Well it is a table of keys and their respective mappings.

### Key
The key to bind the action to in standard vim notation (`:h key-notation`) Note that all keys in Ido are *single* keybinds only. In simpler terms, **NO KEYCHORDS ALLOWED**.

### Mapping
The action which is bound to the key. It can be one of the following as described below

A function:
```lua
config.set{
   keys = {
      ["<C-b>"] = function ()
         require("ido.cursor").forward_word()
      end
   }
}
```

A builtin Ido function which is characterised as:

`ido.MODULE_NAME.FUNCTION_NAME`

```lua
config.set{
   keys = {
      ["<C-b>"] = "ido.cursor.forward_word"
   }
}
```

A lua string:
```lua
config.set{
   keys = {
      ["<C-b>"] = "require('your_module').your_function()"
   }
}
```
