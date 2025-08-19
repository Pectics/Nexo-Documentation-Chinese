# 🐴 自定义生物盔甲 (1.21.2+)

Nexo 允许你自动生成多种类型的生物盔甲。
主要包括狼盔甲、马盔甲和羊驼盔甲。它们遵循与 [components.md](../custom-armors/components.md "mention") 玩家盔甲相同的模式，其中物品 ID 和盔甲纹理的命名规则分别为：`armorname_wolf_armor`、`armorname_horse_armor` 和 `armorname_llama_armor`。

```yaml
forest_wolf_armor:
  itemname: "Forest Wolf Armor"
  material: WOLF_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_wolf_armor_icon
    CustomArmor:
      wolf_armor: nexo:item/nexo_armor/forest_wolf_armor
forest_llama_armor:
  itemname: "Forest Llama Carpet"
  material: PAPER
  Pack:
    texture: nexo:item/nexo_armor/forest_llama_armor_icon
    CustomArmor:
      llama_armor: nexo:item/nexo_armor/forest_llama_armor
forest_horse_armor:
  itemname: "Forest Horse Armor"
  material: DIAMOND_HORSE_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_horse_armor_icon
    CustomArmor:
      horse_armor: nexo:item/nexo_armor/forest_horse_armor
```
