example - Hide code between `--[[NO_SHOW]]` and `--[[END]]` markers in the output.
```lua
--[[NO_SHOW]]
local a = 1
--[[END]]
print(a)
--[[NO_SHOW]]
print(a+1)
--[[END]]
```
Output - this should not show up in docs or be a button.
```lua
--[[NO_EXECUTE]]
print(a)
```

Custom name
```lua
--[[name: my custom name]]
print("This code block has a custom name")
```

#Header priority

example
```lua
print("This code block is labeled based on the nearest header above it")
```