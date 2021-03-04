# Acceptation
The purpose of a narrowing framework is to *select* an item from a list of items. This is the module which deals with all the acceptation work that Ido does.

This is a module which you will probably never use. The only scenario it *might* come in useful is if you wish to extend the behaviour of Ido via [advices](advice.md).

Load the module
```lua
local accept = require("ido.accept")
```

## `accept.selected()`
Accept the selected result. This is a simple function, all it does is stop the event loop of Ido. It is bound to `<CR>` by default.

Advices:
- `stop_event_loop` Stop the event loop of Ido once a result has been accepted

- `no_results` There is no result which can be accepted

- `accept` Accept the result

Return:
- `true`

## `accept.suggestion()`
Accept the suggestion offered. A *suggestion* is a common string which is present after the last matched position in all results which match the query **non fuzzily**. If using the default layout, it is displayed within square brackets (`[]`) right after the query. This action is bound to `<Tab>` by default.

There is another scenario where suggestions are activated, when there is only *one* matching item. The rationalisation behind this has to do the UNIX shell, especially interactive shells like `bash`, `zsh` and the like. When there is only one possible autocompletion, hitting TAB completes it. Therefore in Ido, if there is only one result, hitting the keybinding for the suggestion key will accept it. In fact, when there is only one result, it won't be displayed as normal. Rather it will be displayed as a suggestion, where you can use either the "accept selected" key or the "accept suggestion" key.

Advices:
- `no_suggestion` There is no suggestion which can be accepted

- `single_result` There is only one result, accepts the selected result

- `append_to_query` Append the suggestion text to the query

- `fetch_results` Fetch the results after appending the suggestion

- `single_results_after_fetching` After fetching the results, only one result is found

- `clear_suggestion` Clear the suggestion variable

Return:
- `true`
