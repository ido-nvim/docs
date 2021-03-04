# Results
The module which deals with the results of the narrowing.

Load it
```lua
local result = require("ido.result")
```

## `result.fetch()`
Makes a call to a customized version of the `filter()` function of the [LuaJIT bindings](https://github.com/romgrk/fzy-lua-native) to the [fzy](https://github.com/jhawthorn/fzy) algorithm. It fetches the results, generates the suggestion, sorts the results according to their scores and renders Ido.

Advices:
- `filter` Filter the items

- `empty_query` The query is item, just do a modified copy of the table

- `no_results` No results were found after filtering

- `single_result` Single result was found after filtering

- `render` Render after filtering the items

## `result.next()`
Switch the selected result to the next result if there is any

Advices:
- `not_found` There is no next result to switch to

- `switch` Increment the index of the selected item and wrap it around the limits

- `render` Render after switching to the next item

## `result.prev()`
Switch the selected result to the previous result if there is any

Advices:
- `not_found` There is no previous result to switch to

- `switch` Decrement the index of the selected item and wrap it around the limits

- `render` Render after switching to the previous item
