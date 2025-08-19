---
description: MythicMobs 允许你创建带有高级技能和属性的自定义生物与 Boss
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966831974004174858/unknown.png
coverY: 0
---

# MythicMobs - 自定义生物

MythicMobs 是一个用于创建高度自定义的生物和 Boss 的插件。\
本页将解释如何让这些生物掉落 NexoItem，或者为它们装备 NexoItem。

下面是一个定义装备和掉落的配置示例（同样适用于掉落表 DropTables）：

```yaml
ExampleMob:
  Type: WITHER_SKELETON
  Equipment:
    - IRON_HELMET HEAD
    - nexo:forest_sword HAND
    - nexo:forest_shield OFFHAND
  Drops:
    - nexo forest_chestplate 1to2 1.0
    - # nexo itemid 数量 概率
```
