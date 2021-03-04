# Docs
The official documentation for the [core](https://github.com/ido-nvim/core) of Ido.

## Basic usage
```vim
:lua require("ido.main").start{items = {"red", "green", "blue"}}
```

In place of `{"red", "green", "blue"}`, place the items you wish to narrow.

## API Documenation
Explains the files in the core of Ido.

- [Ido](ido.md)
- [Configuration](config.md)
- [Motions](motion.md)
- [Cursor](cursor.md)
- [Delete](delete.md)
- [Layouts](layout.md)
- [Themes](theme.md)
- [Main](main.md)
- [Event](event.md)
- [Renderer](render.md)
- [Results](result.md)
- [Acceptation](accept.md)
- [Advices](advice.md)
- [Modules](module.md)
- [Packages](package.md)

## Examples
Demonstrates real world applications of the features developed in Ido.

- [Layouts](ex_layout.md)
- [Themes](ex_theme.md)
- [Advices](ex_advice.md)
- [Modules](ex_module.md)
- [Packages](ex_package.md)

## Source code
If this is not enough for you, read the source code of [core](https://github.com/ido-nvim/core). Because the source code will *always* be the first-class citizen in a project. The comments serving as documentation in the code will forever be maintained and updated.
