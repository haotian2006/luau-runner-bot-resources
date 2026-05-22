`wait()` is an deprecated method that is check every 30 hz. `task.wait()` is the newer and more accurate method that is check every frame, which is typically 60 hz. This means that `task.wait()` will be more responsive and accurate than `wait()`.

Example
```lua
local startTime = os.clock()
for i = 1,60 do
    task.wait()
end
-- Should take ~1 second 
print(`task.wait() took: {os.clock() - startTime}s`)
local startTime = os.clock()
for i = 1,60 do
    wait()
end
-- Should take ~2 seconds because wait() is check every
-- 30 hz, and 60 * 1/30 = 2 
print(`wait() took: {os.clock() - startTime}s`)
```