Generalised iteration allows you to iterate over arrays and dictionaries, without needing to use `ipairs` or `pairs`. It has the same iteration order as `next`/`pairs`. It will also be in-order for arrays as luau has made arrays more reliable and consistent compared to Lua where using pairs on arrays could lead to out-of-order iteration.

example
```lua
local array = {1, 2, 3}
local dictionary = {a = 1, b = 2, c = 3}

print("OLD: USING ipairs and pairs")
for index, value in ipairs(array) do
    print(index, value)
end

for key, value in pairs(dictionary) do
    print(key, value)
end

print("NEW: USING GENERALISED ITERATION")
for index, value in array do
    print(index, value)
end

for key, value in dictionary do
    print(key, value)
end
```
