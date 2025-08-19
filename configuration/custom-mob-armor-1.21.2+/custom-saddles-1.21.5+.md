# 🐖 自定义鞍具 (1.21.5+)

当使用 COMPONENT 类型的自定义盔甲时，Nexo 允许你为多种生物轻松创建自定义鞍具。支持的实体包括：**骆驼、驴、马、骡、猪、骷髅马、炽足兽以及僵尸马**。

与其他自定义盔甲部分类似，命名模式为 `mobtype_saddle`。

```yaml
forest_saddle:
  itemname: Forest Saddle
  type: SADDLE
  Pack:
    texture: nexo:items/forest_armor/forest_saddle_icon
    CustomArmor:
      pig_saddle: nexo:items/forest_armor/forest_pig_saddle
      horse_saddle: nexo:items/forest_armor/forest_horse_saddle
  Components:
    equippable:
      slot: BODY
      allowed_enity_types: [ PIG, HORSE ]
```

这里的 `Pack.CustomArmor.x_saddle` 指向我们存放鞍具本体纹理的位置，而 `Pack.texture` 则是图标。
同时我们还需要在 EquippableComponent 中设置 `allowed_entity_types`，以便 Nexo 正确处理剩余的属性。
