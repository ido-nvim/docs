# Modules
This document will guide you through creating your first Ido module.

## Setup

- Go to a directory which is in the Neovim lua load path

```console
$ cd ~/.config/nvim/lua
```

- Create a file, let's call it `test.lua`

```console
$ touch test.lua
```

- Write down the *lua module* boilerplate

```lua
-- @file test.lua

local test = {}

return test
```

- Ready. Set. Go!

## The `main()` function
This is the entry point of any Ido module. This is optional, it is only required in modules which are supposed to be run. You can very well have modules which only define layouts or themes.

Let's create a basic function which helps us narrow out files and directories in the `HOME` directory

```lua
-- @file test.lua

local ido = require("ido")

function test.main()
   print(ido.start{
      items = vim.fn.systemlist("ls $HOME")
   })
end
```

That's the entry point of our module, just like the `main()` method is the entry point in a C program.

Let's test it out then. Restart your NeoVim instance and load the module.

```vim
:lua require("ido").module.load{name = "test"}
```

Everything's fine and good. Now run the module

```vim
:lua require("ido").module.run("test")
```

It should work just as expected. However there is a small implementation problem with it. *It does not allow for customization*. Let's fix that

## Settings

```lua
-- @file test.lua

test.settings = {
   ls_opts = ""
}

function test.main()
   print(ido.start{
      items = vim.fn.systemlist("ls "..test.settings.ls_opts.." $HOME")
   })
end
```

Behaviour wise, nothing has changed. However now, you can do this:

```vim
:lua require("ido").module.load{name = "test", settings = {ls_opts = "-A"}}
```

Now it will list all hidden files as well.

## Options
What if you want some [options](config.md) to be set in the module, but don't want to litter the `ido.start()` function? Just use options!

```lua
-- @file test.lua

test.options = {
   prompt = "Files: ",

   word_separators = "/",
}
```

## Disabled options
Normally, you can use something along the lines of the code snippet below to load a module with custom Ido options:

```vim
:lua require("ido").module.load{name = "test", options = {word_separators = " /?"}}
```

But what if you want some specific options to be "disabled", that is to say they are not changeable from the point of `ido.module.load()`

```lua
test.disabled = {
   word_separators = true
}
```

Try loading the module now with a custom `word_separators` value.

## Binding
If you wish to bind the test module to a keymapping, say `<Leader>.`, you *can* do something along the lines of:

```vim
noremap <Leader>. :lua require("ido").module.run("test")
```

However this is additional overhead which you need not worry yourself with, considering Ido already handles this for you.

- Hardcode it into the module:

```lua
-- @file test.lua

test.binding = {
   key = "<Leader>."
}
```

- Or you can specify it when loading the module:

```vim
:lua require("ido").module.load{name = "test", binding = {key = "<Leader>."}}
```

- This will bind our `test` module to `<Leader>.` as if you had used `noremap`

- Custom modes:

```lua
-- @file test.lua

test.binding = {
   key = "<Leader>."
   mode = "normal"
}
```

| Name | Description | VimL equivalent |
| ---- | ----------- | --------------- |
| `major` | Normal, visual, select and operator modes | `noremap` |
| `normal` | Normal mode | `nnoremap` |
| `visual` | Visual mode | `vnoremap` |
| `select` | Select mode | `snoremap` |
| `operator` | Operator-pending mode | `onoremap` |
| `command` | Command mode | `cnoremap` |
| `insert` | Insert mode | `inoremap` |
| `terminal` | Terminal mode | `tnoremap` |

## Packages
Modules are the building blocks of an entity known as a "Ido package". Find out how you can create one [here](ex_package.md)
