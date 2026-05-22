When resuming a thread that was yielded inside an engine-managed execution context (such as `RemoteFunction.OnServerInvoke`, `BindableFunction.OnInvoke`, `game:BindToClose`, or during `require(ModuleScript)` execution) using `coroutine.resume`, the engine may fail to correctly restore or maintain the internal continuation state associated with that execution frame. This can result in the original caller to remain suspended indefinitely even though the coroutine itself completes execution.

This issue does not occur when resuming the thread via scheduler-managed APIs such as `task.spawn` or `task.defer`, which re-enter the Roblox task scheduler and preserve engine continuation semantics.

Case 1 - Resuming a thread yielded inside `BindableFunction.OnInvoke` using `coroutine.resume`:
```lua
local bindable = Instance.new("BindableFunction")
bindable.OnInvoke = function()
    local thread = coroutine.running()

    task.delay(1, function()
        coroutine.resume(thread)
    end)

    coroutine.yield()
    print("RESUMED") -- prints after 1 second
    return "RETURNED"
end
print(bindable:Invoke()) -- never prints
print('FINISH') -- never prints
```

Case 2 - Resuming a thread yielded inside `BindableFunction.OnInvoke` using `task.spawn`:
```lua
local bindable = Instance.new("BindableFunction")
bindable.OnInvoke = function()
    local thread = coroutine.running()

    task.delay(1, function()
        task.spawn(thread)
    end)

    coroutine.yield()
    print("RESUMED") -- prints after 1 second
    return "RETURNED"
end
print(bindable:Invoke()) -- prints "RETURNED" after 1 second
print('FINISH') 
```