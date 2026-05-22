These are resources for the bot's tag command. They are written in markdown. To contribute, simply open a pull request editing these files.

## Code block markers

Markers placed inside ` ```lua ` / ` ```luau ` code blocks to control how they appear and run in Discord.

| Marker | Effect |
|---|---|
| `--[[NO_EXECUTE]]` | Block displays in the embed but gets no run button |
| `--[[NO_SHOW]]` ... `--[[END]]` | Block is hidden from the embed but still runs when the button is clicked |
| `--[[name: your label]]` | Sets a custom label for the run button (must be on the first line of the block) |

## Examples

````markdown
```lua
--[[name: Print Hello]]
--[[NO_SHOW]]
log("Running example", "cyan", true)
--[[END]]
print("Hello!")
```
````

This produces a run button labeled **Print Hello**. The `log(...)` line runs when clicked but is hidden from the embed.

---

If no `--[[name:]]` marker is present, the button label is inferred from context above the code block.

````markdown
Case 1 - Building and Customizing Parts
```lua
print("hello")
```
````

Button label: **Case 1** (text before ` - ` is used).

````markdown
# Header 1

Some description text.
```lua
print("hello")
```
````

Button label: **Header 1** (nearest heading wins). This is when `--[[name:]]` is useful for more specific labels.

````markdown
Output
```lua
--[[NO_EXECUTE]]
print(a)
```
````

No button — `--[[NO_EXECUTE]]` marks the block as display-only.
