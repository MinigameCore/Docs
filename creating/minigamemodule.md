---
layout: page
title: MinigameModule
---

A `MinigameModule` is the way that minigames are registered to MinigameCore. A minigame must contain a
`assets/<pluginId>/minigames.json` file with data regarding the minigame. An example file can be found below.

```json
[
    {
        "dependencies" : {
            "minigame_modules" : [
                {
                  "id" : "minigame id",
                  "optional" : false,
                  "version" : "the version of the minigamemodule"
                }
            ],
            "plugins" : [
                {
                  "id" : "plugin id",
                  "optional" : false
                }
            ]
        },
        "id" : "minigamemodule id",
        "main" : "fully qualified class name",
        "name" : "human readable name for the minigamemodule",
        "owner" : "the plugin owner",
        "version" : "the version of the minigamemodule"
    }
]
```
