---
description: Crucible 是 MythicMobs 的一个拓展
cover: >-
  https://git.mythiccraft.io/uploads/-/system/project/avatar/51/unknown.png?width=64
coverY: 0
---

# MythicCrucible

### 将 MythicCrucible 物品导入为 NexoItem

Nexo 与 Crucible 的兼容性允许你将通过 MythicMobs & Crucible 创建的物品导入，并作为 Nexo 物品的基础。\
这样你可以保留在 Crucible 中配置的所有内容，并在此基础上添加你自己的机制、纹理、3D 模型等。

```yaml
example_crucible:
  itemname: "<gradient:#59A7EA:#F1D2FF>Test"
  crucible_id: my_crucible_itemid
```

### 在 Nexo 家具/自定义方块掉落中使用 MythicCrucible 物品

你还可以指定在破坏家具或自定义方块时直接掉落某个 Crucible 物品。
只需像下面这样指定 `crucible_item` 即可：

```yaml
myitemid:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      drop:
        loots:
          - crucible_item: my_crucible_itemid
            amount: 1..3 # 可选
    furniture:
      drop:
        loots:
          - crucible_item: my_crucible_itemid
            amount: 1..3 # 可选
```

### 在 Nexo 配方中使用 MMOItems

你也可以在 Nexo 中创建一个配方，使用 Crucible 物品作为材料或结果。
与掉落相同，只需要指定 `crucible_item`。
下面是一个使用 Crucible 物品的有序合成配方示例。
如果你在游戏内使用 RecipeBuilders 且该物品是 CrucibleItem，它也会自动为你生成。

```yaml
myrecipeid:
  result:
    crucible_item: my_crucible_itemid
  ingredients:
    A:
      crucible_item: my_crucible_itemid
  shape:
  - ___
  - ___
  - _A_
    
```
