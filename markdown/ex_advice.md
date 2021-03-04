# Themes
This document will describe how advices work, with lots and lots of examples.

Before reading this, it is advised to read the [advices api](advice.md) document first.

## Setup
- First of all create a Lua file

```console
$ touch ~/test.lua
```

- Throughout this example the name of the file shall be `test.lua`

- Then write a *simple* function in the file

```lua
local advice = require("ido.advice")

local function say_hello()
   advice.wrap{
      name = "hello_world"
      action = function ()
         print("Hello world")
      end
   }

   print("Outside the advice wrapper")
end
```

- Now call the function at the end of the file

```lua
-- say_hello() definition

say_hello()
```

- Run the file

```console
$ lua test.lua
Hello world
Outside the advice wrapper
```

- You are ready to venture into the unescapable rabbit hole of advices

## `advice.wrap()`
To be clear, what did this function do?

- It took a name: `hello_world`

- It took a function as the action

An advice wrapper *wraps* a function with syntactic sugar. So the call to the wrapper above can be thought of as

```lua
execute_advice_before("hello_world")

execute_advice_overwrite("hello_world") or
   function ()
      print("Hello world")
   end

execute_advice_after("hello_world")
```

See? This function is nothing magical. You pass it a function as an argument. When the wrapper is called, it:

- executes the `before` advice if there is any

- executes the `overwrite` advice if there is any, otherwise it executes the `action`

- executes the `after` advice if there is any

## Add an advice
Now we shall change the behaviour of the `say_hello` function **without changing its definition**

```lua
-- say_hello() definition

-- NOTE: Add this advice before the say_hello() function is called
advice.add{

   target = "say_hello@test:hello_world",

   name = "first_advice"
}

say_hello()
```

This is the basic setup for a new advice. It takes:

- the target, a.k.a. the unique ID of the wrapper

- the name of the advice

The unique ID of the wrapper if it is called inside a function, in case you have forgotten is of the format:

`FUNCTION_NAME@FILE_NAME:WRAPPER_NAME`

So here it would be:

`say_hello@test:hello_world`

That's our target

Now at the moment, our advice doesn't make any change in the behaviour of the `say_hello` function whatsoever. Let's check it out just to be sure.

```console
$ lua test.lua
Hello world
Outside the advice wrapper
```

Let's make a change in the behaviour then

```lua
-- say_hello() definition

advice.add{

   target = "say_hello@test:hello_world",

   name = "first_advice",

   action = function ()
      print("The first advice we added")
   end
}

say_hello()
```

The moment of truth. Let's run it!

```console
$ lua test.lua
The first advice we added
Outside the advice wrapper
```

It works! The code inside the advice wrapper has been overwritten by our advice. But what if you don't wish for it to be overwritten? That's when hooks come into play.

Let's add another advice

```lua
-- say_hello() definition

-- first_advice

advice.add{

   target = "say_hello@test:hello_world",

   name = "after_advice",

   hook = "after",

   action = function ()
      print("Execute after the code")
   end
}

say_hello()
```

Let's run it

```console
$ lua test.lua
The first advice we added
Execute after the code
Outside the advice wrapper
```

That's how hooks in advices works.

- You specify the type: `before`, `after` or `overwrite`

- The advice will be executed on the hook

BTW in the first advice, we noticed it overwrote the default code right? That's the `overwrite` hook in action. By default all the functions in the advices api will default to `overwrite` if the hook is not supplied.

I would show the `before` advice, however it would be kind of redundant, considering the `after` advice has been demonstrated. The `before` advice is like that. It will activate, you know, *before* the default/overwrite action.

## Multiple advices
You can have multiple advices on the same hook. They will get executed in a chronological order, based on the time when it was added. The advice added first will get activated first, the second one second, the third third, yada yada yada. It basically works on a First-Come-First-Serve basis.

For example, let's add another after advice

```lua
-- say_hello() definition

-- first_advice

-- first `after` advice

-- second `after` advice
advice.add{

   target = "say_hello@test:hello_world",

   name = "after_advice_2",

   hook = "after",

   action = function ()
      print("Execute after the 'after' advice #1")
   end
}

say_hello()
```

Let's run it

```console
$ lua test.lua
The first advice we added
Execute after the code
Execute after the 'after' advice #1
Outside the advice wrapper
```

## Remove
Let's remove the overwrite advice

```lua
-- say_hello() definition

-- first_advice

-- first `after` advice

-- second `after` advice

advice.remove{

   target = "say_hello@test:hello_world",

   name = "first_advice",

}

say_hello()
```

Let's run it

```console
$ lua test.lua
Hello world
Execute after the code
Execute after the 'after' advice #1
Outside the advice wrapper
```

It is removed.

Let's remove the `after` advice #2

```lua
-- say_hello() definition

-- first_advice

-- first `after` advice

-- second `after` advice

-- first advice removal

advice.remove{

   target = "say_hello@test:hello_world",

   name = "after_advice_2",

   hook = "after"
}

say_hello()
```

Let's run it

```console
$ lua test.lua
Hello world
Execute after the code
Outside the advice wrapper
```

## Temporary
Advices can be of two types:

- `temporary` Once the advice is executed once, it will get removed

- `permanent` The advice won't be removed, unless `advice.remove()` is used. This is the default type

Let's create a temporary advice

```lua
-- say_hello() definition

-- first_advice

-- first `after` advice

-- second `after` advice

-- first advice removal

-- after advice #2 removal

-- Demonstrate the `before` advice to kill two birds with one stone
advice.add{

   target = "say_hello@test:hello_world",

   name = "before_advice",

   hook = "before",

   action = function ()
      print("The before advice")
   end,

   temporary = true
}

say_hello()

print("\n================\n")

say_hello()
```

Let's run it

```console
$ lua test.lua
The before advice
Hello world
Execute after the code
Outside the advice wrapper

================

Hello world
Execute after the code
Outside the advice wrapper
```

That's how temporary advices work

## Global namespace
Advice wrappers in the global namespace have an ID of the form

`FILE_NAME:WRAPPER_NAME`

Let's get rid of everything in the `test.lua` because it is getting messy, and start from scratch.

```lua
local advice = require("ido.advice")

advice.wrapper{
   name = "advice_in_global_namespace",

   action = function ()
      print("Hello world")
   end
}
```

Let's run it

```console
$ lua test.lua
Hello world
```

Let's add an advice

```lua
local advice = require("ido.advice")

-- NOTE: Add this *before* the advice wrapper is called
advice.add{
   name = "bye_bye",

   target = "test:advice_in_global_namespace",

   action = function ()
      print("Bye Bye!")
   end
}

advice.wrapper{
   name = "advice_in_global_namespace",

   action = function ()
      print("Hello world")
   end
}
```

Note how the advice is added *before* the wrapper is called. This is important.

Let's run it

```console
$ lua test.lua
Bye Bye!
```

No hook was supplied, so it defaulted to `overwrite`.

## Extend Ido
Most of the Ido files have been written with extensive capabilities in mind. Check out their respective API documentations to find out more.
