# Files and folders naming guidelines
This describes how file paths should look like for better readability and expandability.

## File paths should use [kebab-case](https://en.wiktionary.org/wiki/kebab_case)
#### Good
```lua
-- garrysmod/addons/my-addon/lua/autorun/my-addon.lua
```

#### Bad
```lua
-- garrysmod/addons/MyAddon/lua/autorun/myaddon.lua
-- garrysmod/addons/MYAdDOn/lua/autorun/shared.lua
-- garrysmod/addons/Myaddon/lua/autorun/sh_myaddon.lua
-- garrysmod/addons/myaddon/lua/autorun/sh_addon.lua
```

## Code initialization files must contain explicit indications of association with a particular code realm.
#### Good
```lua
-- garrysmod/addons/my-addon/lua/my-addon/client/init.lua
-- garrysmod/addons/my-addon/lua/my-addon/cl_init.lua
-- garrysmod/addons/my-addon/lua/my-addon/client.lua

-- garrysmod/addons/my-addon/lua/my-addon/server/init.lua
-- garrysmod/addons/my-addon/lua/my-addon/server/sv_init.lua
-- garrysmod/addons/my-addon/lua/my-addon/server.lua
-- garrysmod/addons/my-addon/lua/my-addon/init.lua

-- garrysmod/addons/my-addon/lua/my-addon/shared/init.lua
-- garrysmod/addons/my-addon/lua/my-addon/shared/sh_init.lua
-- garrysmod/addons/my-addon/lua/my-addon/shared.lua

-- garrysmod/addons/my-addon/lua/my-addon/core/init.lua
```

#### Bad, paths in the example do not have an explicit belonging to any game realm, which makes code analysis and its structure more difficult.
```lua
-- garrysmod/addons/my-addon/lua/my-addon/startup1.lua
-- garrysmod/addons/my-addon/lua/my-addon/internal.lua
-- garrysmod/addons/my-addon/lua/my-addon/my-addon.lua
-- garrysmod/addons/my-addon/lua/my-addon/wow.lua
```
