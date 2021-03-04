# Ido
This is the aliases file. Meant for convenience. This document assumes you have read the other documents.

Load the module
```lua
local ido = require("ido")
```

## `ido.setup(OPTIONS)`
This is a combination of the `package.setup` and the `config.set` functions.

It takes a table of options.

Fields:
- `default` The default options which is passed to `config.set`

- `packages` The packages configuration which is passed to `package.setup`

Returns:
- `true`

## `ido.start()`
Alias to `main.start`

## Other aliases
- `ido.main` alias for [ido/main](main.md)
- `ido.theme`alias for [ido/theme](theme.md)
- `ido.config`alias for [ido/config](config.md)
- `ido.layout`alias for [ido/layout](layout.md)
- `ido.module`alias for [ido/module](module.md)
- `ido.advice`alias for [ido/advice](advice.md)
- `ido.cursor`alias for [ido/cursor](cursor.md)
- `ido.motion`alias for [ido/motion](motion.md)
- `ido.delete`alias for [ido/delete](delete.md)
- `ido.render`alias for [ido/render](render.md)
- `ido.result`alias for [ido/result](result.md)
- `ido.accept`alias for [ido/accept](accept.md)
- `ido.package`alias for [ido/package](package.md)
