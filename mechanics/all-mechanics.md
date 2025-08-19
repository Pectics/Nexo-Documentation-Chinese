---
description: 默认可用的不同机制及其配置，按类别分类
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# 其他机制

## 杂项

### 背包

这个机制允许你把任何物品变成背包。

{% hint style="info" %}
此机制可能会导致物品复制问题！
如果你发现任何问题，请提交一个 [bug-report](all-mechanics.md)，我们会尽快修复！\\
{% endhint %}

```yml
backpack:
  itemname: backpack
  material: PAPER
  Components:
    max_stack_size: 1
  Mechanics:
    backpack:
      rows: 4
      title: "<red>Backpack"                      #可选，默认值: "Backpack"
      open_sound: "entity.shulker.open"       #可选，默认值: "entity.shulker.open"
      close_sound: "entity.shulker.close"     #可选，默认值: "entity.shulker.close"
```

### 杂项机制

{% hint style="warning" %}
在 1.20.5+ 中请使用新的 [FireResistant-Component](../configuration/items-advanced.md) 来替代 **burns\_in\_x**
{% endhint %}

这个机制允许你对物品进行一系列小改动。
每一项的功能基本上是自解释的。

```yaml
myitem:
  Mechanics:
    misc:
      breaks_from_cactus: true
      burns_in_fire: true
      burns_in_lava: true
      disable_vanilla_interactions: false
      can_strip_logs: false
      piglins_ignore_when_equipped: false
      compostable: false
      allow_in_vanilla_recipes: true
```

### 指令

这个机制允许你执行指令（以控制台、玩家或 OP 玩家身份）。虽然这种方式不总是最优雅的，但它简化了很多操作。你可以设置冷却时间、检查玩家是否拥有特定权限，并在执行指令时消耗物品（减少数量）。

```yaml
myitem:
  Mechanics:
    commands:
      cooldown: 5 # 示例冷却时间（秒）。可选
      permission: "my.awesome.perm" # 所需权限。可选
      one_usage: true # 使用时是否消耗物品数量？默认: false
      console:
        # 例如：杀死玩家
        - "kill %p%"
      player:
        # 例如：玩家执行 /spawn
        - "spawn"
      opped_player:
        # 例如：玩家给予自己一把钻石剑
        - "give diamond_sword 1"
```

### 盔甲效果

这个机制允许你将药水效果绑定到盔甲（或头盔），装备时即可获得对应效果。
[这里](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/potion/PotionEffectType.html) 有所有药水效果类型的列表。

```yaml
myitem:
  Mechanics:
    armor_effects:
      night_vision: # 药水效果类型
        duration: 10
        amplifier: 0
        ambient: true # 使药水效果产生更多半透明粒子
        particles: true # 是否显示粒子
        icon: true # 是否显示图标
```

你还可以让效果仅在穿戴整套装备时生效。

```yaml
myitem:
  Mechanics:
    armor_effects:
      night_vision:
        requires_full_set: true
        ...
```

### clickAction

这个机制允许你在玩家点击方块或家具时触发各种事件。它非常灵活，因此有一个 [专门的教程页面](clickaction-mechanic.md)。

### ItemType

使用这个机制，你可以更改 NexoBlocks 检测到的物品类型。请确保使用的是 [音符盒机制](custom-block-mechanics/noteblock-mechanic/#global-configuration) 中声明的类型。

```yaml
myitem:
  Mechanics:
    itemtype:
      value: SUPER_MATERIAL # 你的 itemType
```

### 灵魂绑定

通过这个机制，你可以让玩家在死亡时不掉落该物品。

```yaml
myitem:
  Mechanics:
    soulbound:
      lose_chance: 0
```

### 自定义机制

这个机制允许你自定义事件、条件和动作。
由于它比较特殊，所以有一个 [专门的教程页面](custom-mechanic.md)。

## 战斗

### 雷神 (Thor)

你是否曾梦想能召唤闪电？这个机制可以满足你。

```yaml
myitem:
 Mechanics:
   thor:
    lightning_bolts_amount: 5
    random_location_variation: 1.5
    delay: 20000 # 毫秒 (20000ms = 20s)
```

* **lightning\_bolts\_amount**: 生成的闪电数量
* **random\_location\_variation**: 闪电间的随机位置偏差范围（以方块为单位）
* **delay**: 使用间的冷却时间，单位毫秒（1000ms = 1s）

### 吸血 (Lifesteal)

想在攻击敌人时偷取生命值吗？

```yaml
myitem:
  Mechanics:
    lifesteal:
      amount: 2 # 你将从对手身上偷取的半颗心数量
```

### 能量冲击 (EnergyBlast)

EnergyBlast 是一个很酷的机制，会生成一个粒子锥形区域来攻击实体。

```yaml
myitem:
  Mechanics:
    energyblast:
      delay: 20000
      length: 5
      damage: 10.0
      particle:
        type: REDSTONE # 只有 REDSTONE 粒子可以改变大小和颜色
        size: 1
        color:
          red: 0
          green: 255
          blue: 255
```

### 凋灵之首 (Witherskull)

右键点击即可发射凋灵骷髅头！

```yaml
myitem:
  Mechanics:
    witherskull:
      charged: false # 是否为充能状态，充能的骷髅头可以破坏方块
      delay: 3000 # 毫秒 (3000ms = 3s)
```

## 农业

### 自动收割 (Harvesting)

自动收割并重新种植一定范围内的小麦。

```yaml
myitem:
  Mechanics:
    harvesting:
      cooldown: 10000 # 使用间隔 10 秒
      radius: 5 # 以点击的方块为中心的范围
      height: 3 # 高度范围
```

### 自动熔炼 (Smelting)

挖掘铁矿或金矿时自动熔炼。支持时运和精准采集附魔。

```yaml
myitem:
  Mechanics:
    smelting:
      enabled: true
      play_sound: true
```
