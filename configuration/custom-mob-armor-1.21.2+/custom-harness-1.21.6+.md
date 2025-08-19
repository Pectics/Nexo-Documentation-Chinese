# 🪢 自定义马具 (1.21.6+)

随着全新实体 Happy Ghast 的加入，出现了一种新的装备类型——马具。
Nexo 允许你像 [custom-saddles-1.21.5+.md](custom-saddles-1.21.5+.md "mention") 一样轻松注册自定义马具。

要实现这一点，只需遵循所有 NexoEquipment 的通用模式。下面是一个示例：

```
forest_harness:
  type: PAPER
  itemname: "Forest Harness"
  Pack:
    parent_model: item/generated
    texture: nexo:items/nexo_armor/forest_harness_icon
    CustomArmor:
      harness: nexo:items/nexo_armor/forest_harness
  Components:
    equippable:
      allowed_entity_types: [ HAPPY_GHAST ]
      slot: BODY
```

这里的 `Pack.CustomArmor.harness` 指向我们存放马具本体纹理的位置，而 `Pack.texture` 则是图标。
同时我们还需要在 EquippableComponent 中设置 `allowed_entity_types`，以便 Nexo 正确处理剩余的属性。
