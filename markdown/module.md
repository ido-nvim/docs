# Modules
A module is essentially an Ido extension, a plugin, if you will. It is some syntactic sugar for creating custom third party narrowing functions based on Ido.

Load it

```lua
local module = require("ido.module")
```

## Template
This is the template which all modules follow

| Element | Description |
| ------- | ----------- |
| `options` | Ido [options](config.md) which are set once the module is run |
| `settings` | Module specific settings which can be customized |
| `binding` | The specification for the key binding the module is mapped to |
| `disabled` | The list of Ido options, which cannot be changed using `module.load()` |
| `main` | The entry point of the module, like the `main()` function in C |

## `module.load(OPTIONS)`
This is a function which loads an Ido module. Every time this is called, it will remove the package from `package.loaded`, so that it is a true reload, not a smart reload which lua does by default.

It takes a table of options as an argument

Fields:
- `name` The name of the module, which cannot be `global`. This is mandatory

- `fake_name` The name which will be used when calling `module.run()`. Defaults to `name`

- The elements described in the template above

Returns:
- `nil` if errors were encountered, in which case it will print the cause

- `true` success

## `module.run(NAME, [, ARGS])`
Runs a module.

Params:
- `NAME` The name of the module to run.

- `ARGS` The arguments supplied to the `main()` function of the module.

Returns:
- `nil` if errors were encountered, in which case it will print the cause

- Exit value of the `main` function of the module

## Examples
This document is not for understanding the modules system in Ido. It is merely a reference point for the modules API. To understand modules, see the [examples](ex_module.md)
