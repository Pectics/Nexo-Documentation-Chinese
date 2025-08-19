---
description: 当玩家点击方块或家具时运行指令、播放音效或发送消息。
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# 点击动作机制 (ClickAction Mechanic)

首先，创建一个基础的 [自定义方块](custom-block-mechanics/noteblock-mechanic/) 或 [家具](furniture-mechanic/)。

接着，在 mechanics 部分下，你可以在任意自定义方块或家具机制下添加默认的 clickAction 机制：

```yaml
myitem:
  Mechanics:      
    furniture/custom_block:
      clickActions:
        - conditions:
            - '#player.hasPermission("test.permission")'
          actions:
            - '[console] say <player> hello <player>!'
```

在这个配置下，只有当玩家拥有 `test.permission` 权限时，才会触发控制台执行 `say hello <player>` 指令。

如果你不使用条件，需要在条件位置保留空括号：

```yaml
myitem:
  Mechanics:
    furniture/custom_block:
      clickActions:
        - conditions: []
          actions:
            - '[console] say <player> hello <player>!'
```

### 条件 (Conditions)

条件是高度可配置的。你可以使用 Player 或 Server 的任意 “get” 方法。
所有可用方法的列表可以在 Paper 的 Javadocs 中找到。

{% embed url="https://jd.papermc.io/paper/1.21.8/org/bukkit/entity/Player.html" %}

{% embed url="https://jd.papermc.io/paper/1.21.8/org/bukkit/Server.html" %}
提示！按 "CTRL + F" 并搜索 "get" 来查找可用方法。
{% endembed %}

此外，Spring 文档也是理解如何使用条件表达式的良好资源。

{% embed url="https://docs.spring.io/spring-framework/docs/3.0.x/reference/expressions.html" %}

你还可以通过在条件前添加 `!` 来进行否定检查，例如：

```yaml
myitem:
  Mechanics:      
    furniture/custom_block:
      clickActions:
        - conditions:
            - '!#player.hasPermission("test.permission")'
          actions:
            - '[console] say <player> hello <player>!'
```

这将在玩家没有 **test.permission** 权限时执行该操作。

#### 条件示例

`#server.getOnlinePlayers().size() > 10`

`#server.getAllowEnd()`

`#server.getDefaultGameMode()`

`#player.world.name == 'world'`

`#player.hasPermission("test.permission")`

`#player.gamemode.name() == 'ADVENTURE'`

### 动作 (Actions)

`[console] <command>`

`[player] <command>`

`[message] <message>`

`[actionbar] <message>`

`{source=SOURCE volume=VOLUME pitch=PITCH} [sound] <sound name>`

#### 动作示例

`[console] say hello`

`[player] say hello`

`[message] <blue>Hello!`

`[actionbar] <gray>Hello from the actionbar!`

`{source=AMBIENT volume=0.1 pitch=1} [sound] minecraft:block.shulker_box.close`
