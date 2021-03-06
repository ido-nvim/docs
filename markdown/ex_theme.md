# Themes
This document will describe how themes are created, with lots and lots of examples.

Before reading this, it is advised to read the [themes api](theme.md) document first.

## Default
This is how the default theme is created.

```lua
theme.new{
   name       = "default",
   prompt     = {guifg = "#96a6c8", guibg = "#161616"},
   normal     = {guifg = "#ebdbb2", guibg = "#161616"},
   cursor     = {guifg = "#161616", guibg = "#cc8c3c"},
   ux         = {guifg = "#857c7f", guibg = "#161616"},
   selected   = {guifg = "#d79921", guibg = "#161616"},
   suggestion = {guifg = "#cc8c3c", guibg = "#161616", gui = "bold"},
}
```

Let's check out what that looks like.

![Default theme](img/default.png)

## Concept
Let's use the `prompt` highlight from the above snippet as the example for understanding how this works

```lua
prompt = {
   guifg = "#96a6c8",
   guibg = "#161616"
}
```

The theming api will convert this snippet to the following VimL command

```vim
highlight! ido_prompt guifg=#96a6c8 guibg=#161616
```

Basically, it will loop through every single key in the element, and convert it to a VimL highlight expression, where the name of the highlight is `ido_ELEMENT`.

This is fine and all, but what about links, you say.

```lua
prompt = {
   link = "Function",
}
```

This gets transformed to:

```vim
highlight! link ido_prompt Function
```

Linking something to `Normal` takes less config than you think

```lua
prompt = {}
```

That's it. If an element does not contain any property in it, it will link it to `Normal`

## Buuuuu...but muh VimL
Sure, go ahead. Code stuff in that abysmal language. (No offence Bram)

```vim
highlight! ido_prompt     guifg=#96a6c8 guibg=#161616
highlight! ido_normal     guifg=#ebdbb2 guibg=#161616
highlight! ido_cursor     guifg=#161616 guibg=#cc8c3c
highlight! ido_ux         guifg=#857c7f guibg=#161616
highlight! ido_selected   guifg=#d79921 guibg=#161616
highlight! ido_suggestion guifg=#cc8c3c guibg=#161616 gui=bold
```
