# VS Notifications

Banner notifications for FiveM. No framework required.

## Install

1. Put the `vs_notifications` folder in your resources folder. The folder name has to stay `vs_notifications`.
2. Add this to `server.cfg`, above the resources that send notifications:

```
ensure vs_notifications
```

3. Restart the server, or run `ensure vs_notifications` in the server console.

## Use

From a client script:

```lua
exports['vs_notifications']:Notify('Lock picked', 'success')
exports['vs_notifications']:Notify('Not enough cash.', 'error', 6000)
```

From a server script, pass the player id first:

```lua
exports['vs_notifications']:Notify(source, 'Payment received.', 'success')
```

You can also pass a table:

```lua
exports['vs_notifications']:Notify({
    description = 'Shots reported near Legion Square.',
    type = 'inform',
    duration = 5000,
    id = 'dispatch',
})
```

`id` updates that same banner instead of stacking a new one. The same message and type sent again within `Config.DuplicateWindow` is ignored, unless you pass an `id`.

Types: `success`, `error`, `warning`, `inform`, `info`, `primary`. Anything else is shown as info.

## Config

Edit `config/config.lua`, then restart `vs_notifications`.

| Option | What it does |
| --- | --- |
| `Config.Position` | Where the stack sits. `top`, `top-left`, `top-right`, `bottom`, `bottom-left`, `bottom-right`. Anything else uses `top`. `bottom-left` sits above the minimap. |
| `Config.Duration` | How long a banner stays, in milliseconds. Default `4500`. Shortest is `800`. |
| `Config.Max` | How many banners can be on screen. Default `5`. |
| `Config.DuplicateWindow` | Milliseconds before the same message can show again. Default `300`. |
| `Config.Types` | The word and color for each type. Colors are hex. |

A message longer than 180 characters is cut off.
