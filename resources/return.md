The purpose of `return` is to send data back from a function or exit a function early. Using `return` lets you reuse logic without rewriting it.

Example 1 - Reusing logic with `return`:
```lua
function make_weapon(base_damage, multiplier)
    return base_damage * multiplier
end

function make_enchanted_weapon(base_damage, multiplier, bonus)
    local damage = make_weapon(base_damage, multiplier)
    return damage + bonus
end

local sword = make_enchanted_weapon(10, 2, 5)
local axe = make_enchanted_weapon(15, 1.5, 10)
print(sword, axe)
```

`make_weapon` returns its result so that `make_enchanted_weapon` can build on top of it. Without `return`, there would be no way to pass the result between the two functions.

Example 2 - Exiting early with `return`:
```lua
function output_player_score(player)
    if not player then return  end
    
    local score = player.score
    if score < 0 then return end

    print(`Player score: {score}`)
end

output_player_score(nil) -- does not print anything
output_player_score({score = -5}) -- does not print anything
output_player_score({score = 100}) -- prints "Player score: 100"
```

If we didn't use early `return`, we would have to nest the logic inside multiple `if` statements, which can quickly become hard to read and maintain if there are many conditions to check.

```lua
--[[NO_EXECUTE]]
function output_player_score(player)
    if player then
        local score = player.score
        if score >= 0 then
            print(`Player score: {score}`)
        end
    end
end
```
