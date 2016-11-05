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

A `MinigameModule` must also contain a class annotated with `@MinigameModule`. An example can be found below.

```java
@MinigameModule(
    desciption = "This is the basic layout of a minigame class",
    id = "example_minigame_id",
    minigameDependencies = {
        @Depend.MinigameModule(
            id = "some_minigame",
            optional = false,
            version = "(0.1.0-0.5.2)" // Version range is optional, a single version will work as well.
        )
    },
    name = "Example Minigame",
    plugin = "minigame_plugin_id",
    pluginDependencies = {
        @Depend.Plugin(
            id = "some_plugin",
            optional = true
        )
    },
    version = "0.1.0"
)
public final class ExampleMinigame {

    @Lifecycle
    public void eachStage() {
        // ...
    }

    @Lifecycle.PreInit(order = Order.FIRST)
    public void preInitFirst() {
        // ...
    }

    @Lifecycle.Init(order = Order.LAST)
    public void preInitLast1() {
        // ...
    }

    // This is called after preInitLast1()
    @Lifecycle.Init(order = Order.LAST)
    public void preInitLast2() {
        // ...
    }

}
```

> If there are multiple methods with the same lifecycle annotation and the same order, they will be executed in the
order that they are listed in.
