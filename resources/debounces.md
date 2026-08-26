A **debounce** is a boolean flag that prevents a block of code from running again while it is already running. Without one, rapid repeated calls (e.g. a player spamming a button) can trigger the same logic multiple times simultaneously.

Example 1 - No debounce (broken):
```lua
--[[NO_EXECUTE]]
local function onTouch(part)
    print("touched!")
    task.wait(2)
    print("done")
end

part.Touched:Connect(onTouch)
```

If `part` is touched 5 times in quick succession, `onTouch` fires 5 times at once. Each call runs and prints "touched!" and "done" independently.

Example 2 - With debounce (fixed):
```lua
--[[NO_EXECUTE]]
local debounce = false

local function onTouch(part)
    if debounce then return end
    debounce = true

    print("touched!")
    task.wait(2)
    print("done")

    debounce = false
end

part.Touched:Connect(onTouch)
```

Now the first call sets `debounce = true` and all subsequent calls exit immediately at the `if` check. Once the first call finishes, it resets `debounce = false` so the next touch can go through.

Example 3 - Per-player debounce using a table:
```lua
local debounces = {}
--[[NO_SHOW]]
local button = discord.button("Click me")
--[[END]]
local function onActivated(player)
    if debounces[player] then 
        warn(player," is on cooldown!")
        return 
    end
    debounces[player] = true

    print(player," activated!")
    task.wait(7)
    print(player," cooldown done")

    debounces[player] = false
end

button.Clicked:Connect(function(userId, username)
    onActivated(username)
end)
```

A single `boolean` debounce blocks *all* players. Using a table keyed by player gives each player their own independent cooldown.

Always reset the debounce (`debounce = false`) when the action is finished, or the code will be permanently blocked after the first call.

You can test the code by pressing the `example 3` button multiple times and seeing the cooldown message.
