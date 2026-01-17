# AS Framework

A modern, optimized FiveM framework built with ox_lib integration.

## Features

- 🚀 **Optimized Performance** - Built with ox_lib for maximum efficiency
- 💾 **Database Integration** - Full oxmysql support with auto-save
- 👤 **Player Management** - Complete player data handling and persistence
- 💰 **Money System** - Multi-account money system (cash, bank)
- 💼 **Job System** - Flexible job and grade management
- 🎮 **Multi-Character Support** - Ready for character selection
- 📊 **Metadata System** - Extensible player metadata
- 🔧 **Developer Friendly** - Clean API and easy to extend

## Dependencies

Required resources:
- [ox_lib](https://github.com/overextended/ox_lib)
- [oxmysql](https://github.com/overextended/oxmysql)

## Installation

1. Download and extract `as-core` to your resources folder
2. Add `ensure as-core` to your server.cfg (after ox_lib and oxmysql)
3. Import `database.sql` to your database
4. Configure `shared/config.lua` to your preferences
5. Restart your server

## Configuration

Edit `shared/config.lua` to customize:
- Default money amounts
- Job settings
- Player settings
- Database options
- And more...

## Usage

### Server-side

```lua
-- Get the core object
local AS = exports['as-core']:GetCoreObject()

-- Get a player
local player = AS.Server.GetPlayer(source)

-- Player functions
player.addMoney('cash', 1000)
player.removeMoney('bank', 500)
player.setJob('police', 2)
player.setMeta('hunger', 100)
player.save()

-- Register callbacks
AS.Server.RegisterCallback('myCallback', function(source, cb, data)
    cb({success = true})
end)
```

### Client-side

```lua
-- Get the core object
local AS = exports['as-core']:GetCoreObject()

-- Get player data
local playerData = AS.Client.GetPlayerData()

-- Check if loaded
if AS.Client.IsPlayerLoaded() then
    print('Player is loaded!')
end

-- Use ox_lib helpers
exports['as-core']:ShowNotification({
    title = 'Success',
    description = 'Action completed',
    type = 'success'
})

-- Progress bar
local success = exports['as-core']:ShowProgress({
    duration = 5000,
    label = 'Doing something...',
    useWhileDead = false,
    canCancel = true,
    disable = {
        move = true,
        car = true,
        combat = true
    }
})
```

## Events

### Server Events
- `as-core:server:onPlayerLoaded` - When player loads
- `as-core:server:loadPlayer` - Trigger to load player
- `as-core:server:updatePlayerData` - Update player data
- `as-core:server:updateCoords` - Update player position

### Client Events
- `as-core:client:onPlayerLoaded` - When player loads
- `as-core:client:playerLoaded` - Receive player data
- `as-core:client:onMoneyChange` - Money changed
- `as-core:client:onJobUpdate` - Job changed
- `as-core:client:onMetadataUpdate` - Metadata changed

## Commands

- `/saveall` - Save all player data (admin only)
- `/getplayers` - Get online player count (admin only)

## API Reference

### Server-side Functions

| Function | Description |
|----------|-------------|
| `AS.Server.GetPlayer(source)` | Get player by source |
| `AS.Server.GetPlayerByIdentifier(identifier)` | Get player by identifier |
| `AS.Server.GetPlayers()` | Get all players |
| `AS.Server.SaveAllPlayers()` | Save all players |
| `AS.Server.RegisterCallback(name, cb)` | Register callback |

### Player Object Functions

| Function | Description |
|----------|-------------|
| `player.addMoney(account, amount)` | Add money |
| `player.removeMoney(account, amount)` | Remove money |
| `player.setMoney(account, amount)` | Set money |
| `player.getMoney(account)` | Get money |
| `player.setJob(job, grade)` | Set job |
| `player.getJob()` | Get job |
| `player.setGroup(group)` | Set permission group |
| `player.getGroup()` | Get permission group |
| `player.setMeta(key, value)` | Set metadata |
| `player.getMeta(key)` | Get metadata |
| `player.setCoords(coords)` | Set position |
| `player.getCoords()` | Get position |
| `player.save()` | Save player |
| `player.showNotification(data)` | Show notification |

## Support

For issues and suggestions, please open an issue on GitHub.

## License

MIT License - Feel free to use and modify as needed.
