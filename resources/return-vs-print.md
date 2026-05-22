Many beginners see this pattern:

```lua
--[[NO_EXECUTE]]
function add(a, b)
    return a + b
end
print(add(1, 2))
```

and wonder why not just do this instead:

```lua
--[[NO_EXECUTE]]
function add(a, b)
    print(a + b)
end
add(1, 2)
```

The difference is **flexibility**. The `return` version lets you use the result however you want while `print` can only display it.

Example - Using `print` instead of `return`:
```lua
function add(a, b)
    return a + b
end

local x = add(1, 2)
local y = add(x, 3)
print(x, y)
```

If you replaced `return` with `print` in the above code, you would not be able to store the intermediate result `x` and reuse it to calculate `y`.
