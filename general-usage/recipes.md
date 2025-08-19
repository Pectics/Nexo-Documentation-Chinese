---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966826759293136996/unknown.png
coverY: 0
---

# 🧑‍🍳 配方

配方可以直接在 `Nexo/recipes` 目录中的相关文件里创建，或者通过游戏内的 RecipeBuilder 创建。
RecipeBuilder 可以通过指令 `/nexo recipes builder` 打开。
把你想要的物品拖入工作台槽位中即可生成配方。记得将“输出”槽设置为你想要得到的物品。

### 可用的配方类型：

* SHAPELESS - 无序合成，材料可以放在任意槽位
* SHAPED - 有序合成，需要按照特定形状摆放材料
* FURNACE - 熔炉配方
* BLASTING - 高炉配方
* SMOKING - 烟熏炉配方
* STONECUTTING - 切石机配方
* BREWING - 酿造台配方
* SMITHING - 锻造台配方 —— 通过 [NexoAddon](https://nexoaddon.gitbook.io/docs/recipes/smithing-recipe) 添加

## 示例：

### 无序合成 (Shapeless)

`result` 中的 `amount` 表示你将获得的物品数量

`ingredients` 中的 `amount` 表示该物品需要占用的槽位数量

```yaml
grass_block_shapeless:
  result:
    minecraft_type: GRASS_BLOCK
    amount: 2
  ingredients:
    A:
      amount: 1
      minecraft_type: MOSS_CARPET
    B:
      amount: 2
      minecraft_type: DIRT
```

<div align="left"><figure><img src="../.gitbook/assets/shapeless.png" alt=""><figcaption></figcaption></figure></div>

### 有序合成 (Shaped)

你也可以在配方中使用 Minecraft 的标签以及 Nexo 物品

```yaml
forest_axe:
  result:
    nexo_item: forest_axe
  ingredients:
    A:
      tag: minecraft:leaves
    B:
      minecraft_type: STICK
  shape:
  - _AA
  - _BA
  - _B_

```

<div align="left"><figure><img src="../.gitbook/assets/shaped.png" alt=""><figcaption></figcaption></figure></div>

### 熔炉 + 高炉 + 烟熏炉 (Furnace + Blasting + Smoking)

```yaml
raw_iron_block_to_iron:
  result:
    minecraft_type: IRON_INGOT
    amount: 9
  input:
    minecraft_type: RAW_IRON_BLOCK
  cookingTime: 100
  experience: 20
```

<div align="left"><figure><img src="../.gitbook/assets/smelting.png" alt=""><figcaption></figcaption></figure></div>

### 切石机 (Stonecutting)

```yaml
stripped_spruce_log:
  result:
    minecraft_type: STRIPPED_SPRUCE_LOG
  input:
    minecraft_type: SPRUCE_LOG
```

<div align="left"><figure><img src="../.gitbook/assets/stonecutting.png" alt=""><figcaption></figcaption></figure></div>

### 酿造 (Brewing)

```yaml
diamond:
  result:
    minecraft_type: DIAMOND
  input:
    minecraft_type: GLASS_BOTTLE
  ingredient:
    nexo_item: rainbow_ingot
```

<div align="left"><figure><img src="../.gitbook/assets/brewing.png" alt=""><figcaption></figcaption></figure></div>
