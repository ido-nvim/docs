# Docs
The official documentation for the [core](https://github.com/ido-nvim/core) of Ido.

## Basic usage
```vim
:lua require("ido").start{items = {"red", "green", "blue"}}
```

In place of `{"red", "green", "blue"}`, place the items you wish to narrow

## API Documenation
Explains the files in the core of Ido.

- [Ido](markdown/ido.md)
- [Configuration](markdown/config.md)
- [Motions](markdown/motion.md)
- [Cursor](markdown/cursor.md)
- [Delete](markdown/delete.md)
- [Themes](markdown/theme.md)
- [Main](markdown/main.md)
- [Event](markdown/event.md)
- [Render](markdown/render.md)
- [Results](markdown/result.md)
- [Acceptation](markdown/accept.md)
- [Advices](markdown/advice.md)
- [Modules](markdown/module.md)
- [Packages](markdown/package.md)

## Examples
Demonstrates real world applications of the features developed in Ido.

- [Themes](markdown/ex_theme.md)
- [Advices](markdown/ex_advice.md)
- [Modules](markdown/ex_module.md)
- [Packages](markdown/ex_package.md)

## Source code
If this is not enough for you, read the source code of [core](https://github.com/ido-nvim/core). Because the source code will *always* be the first-class citizen in a project. The comments serving as documentation in the code will forever be maintained and updated.
