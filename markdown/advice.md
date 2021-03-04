# Advices
Advices are a concept which has its origins in the [Lisp](https://en.wikipedia.org/wiki/Lisp_(programming_language)) family of programming languages. It is essentially a method of modifying the behaviour of a piece of code with some custom behaviour *without changing the code itself*.

![Illustration](advice.png)

First of all load the `advices` module of Ido

```lua
local advice = require("ido.advice")
```

## `advice.wrap(OPTIONS)`
Wraps an advice function around a piece of code, and gives the code a unique ID. This is the function which acts as the *executor*, if you will. When a piece of code is wrapped in this by means of a lambda, it will do three things:

- Check if there is a function which is associated with the ID of the wrapper and has the hook of `before` and execute it
- Check if there is a function with the hook of `overwrite` and execute it, else execute the piece of code associated with it
- Check if there is a function with the hook of `after` and execute it

The ID of an advice wrapper depends on three things:

- The name of the function the advice is defined within
- The name of the file without the `.lua` where the advice is defined in
- The name of the wrapper supplied as a parameter

If it gets all of these, the ID of the advice wrapper will be:\
`FUNCTION_NAME@FILE_NAME:WRAPPER_NAME`

If the wrapper is invoked in the global namespace and not inside a function, then the ID will be:\
`FILE_NAME:WRAPPER_NAME`

It takes a table of options as an argument

Fields:
- `name` The name of the wrapper. See above for details

- `action` The piece of code supplied as a function, either a *true defined function* or a *lambda*. This is optional

Returns:
- `nil` Some errors have occured. In this case, it will print out the exact cause of the error

- `true` No errors have occured

## `advice.add(OPTIONS)`
Adds an advice to be executed by the wrapper. Note that this needs to be executed before the advice wrapper is *executed*, otherwise it won't work. Of course, if the advice wrapper is in a function, then it is safe to call this *before* that function is called.

It takes a table of options as an argument

Fields:
- `name` The name of the advice, used when calling `advice.remove()`

- `target` The unique ID of the advice wrapper, see above for details

- `action` The piece of code which is being advised. Can be a defined function or a lambda

- `temporary` Whether the advice will be removed once it is executed once, `false` by default

- `hook` The hook when the advice will be executed, can be one of `before`, `after` or `overwrite` (default)

Returns:
- `nil` Some errors have occured. In this case, it will print out the exact cause of the error

- `true` No errors have occured

## `advice.remove(OPTIONS)`
Removes an advice from the list of advices which get executed by the advice wrapper. Like with `advice.add` above, this needs to be executed *before* the advice wrapper is.

It takes a table of options as an argument

Fields:
- `name` The name of the advice

- `target` The unique ID of the advice wrapper

- `hook` The hook when the advice will be executed, `overwrite` by default

Returns:
- `nil` Some errors have occured. In this case, it will print out the exact cause of the error

- `true` No errors have occured
