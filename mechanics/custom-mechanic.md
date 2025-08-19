---
description: 该机制允许你在无需编程的情况下实现一个高度可自定义的机制
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# 自定义机制 (Custom Mechanic)

## 它是如何工作的？

该机制仅适用于物品，不适用于方块或家具。
方块/家具请查看 [点击动作机制](clickaction-mechanic.md)。
自定义机制允许你创建由三部分组成的小节：

* **Event（事件）**：该机制何时触发？例如，当你右键点击方块时
* **Conditions（条件）**：必须满足的一组条件。例如，拥有某个权限
* **Actions（动作）**：要执行的一组动作。例如，发送一条指令或消息

{% hint style="info" %}
一个名为 one\_usage 的可选设置可以让你模拟物品的一次性使用。
{% endhint %}

## 一个完整的示例

```yaml
myitem:
  Mechanics:
    custom:
      test:
        one_usage: false
        event: "CLICK:right:all"
        conditions:
          - '#player.hasPermission("example.permission")'
        actions:
          - "[console] give <player> cooked_beef 1"
```

在此示例中，小节 `test` 定义了一个自定义机制，当有人右键点击（无论是方块还是空气）时触发。
如果该玩家拥有 `example.permission` 权限，控制台将执行 give 指令，并将 \<player> 替换为玩家名字。
物品不会被消耗（one\_usage: false）。

## 可用事件

### CLICK\:click\_type\:target\_type, DROP[^2], PICKUP[^3], BREAK[^4], EQUIP[^5], UNEQUIP[^6], INV\_CLICK[^7], DEATH[^8]

## 可用条件

### HAS\_PERMISSION\:the.permission

**the.permission**: `使用该物品的玩家所需的权限`

## 可用动作

### Command-Action

该动作允许你以控制台或玩家的身份运行命令

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "[console] minecraft:give <player> minecraft:paper 2"
```

### Message-Action

该动作允许你向玩家发送一条可自定义的消息

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "[message] <red>some message <gradient:red:blue>with MiniMessage support"
```

### ActionBar-Action

该动作允许你向玩家发送一条可自定义的 ActionBar 消息

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "[actionbar] <red>some message <gradient:red:blue>with MiniMessage support"
```

### Sound-Action

该动作允许你在某个位置或目标处播放一个音效，并支持自定义参数

**source -** 音效来源 ([来源列表](https://jd.advntr.dev/api/4.21.0/net/kyori/adventure/sound/Sound.Source.html))
**volume** - 播放音效的音量
**pitch** - 播放音效的音调
**self** - 如果为 true，则在玩家处播放，而不是在某个位置播放

紧随其后的是要播放的音效键值

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "{source=AMBIENT volume=0.1 pitch=1} [sound] namespace:soundkey"
```

[^1]: 当你使用物品点击时触发。

    **mouse\_click\_type**: `[ right, left, all ]`
    **target\_type**: `[ block, air, all ]`

[^2]: 当你丢弃物品时触发。

[^3]: 当你拾取物品时触发。

[^4]: 当玩家破坏物品时触发。

[^5]: 当玩家装备物品时触发。

[^6]: 当玩家卸下物品时触发。

[^7]: 当玩家在物品栏中点击物品时触发。

[^8]: 当玩家死亡并且通常会掉落该物品时触发。
