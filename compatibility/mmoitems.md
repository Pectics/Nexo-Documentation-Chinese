---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966832308395049000/unknown.png
coverY: 0
---

# MMOItems

### 将 MMOItem 导入为 NexoItem

Nexo 与 MMOItems 的兼容性允许你导入由该插件创建的物品，并将其作为 Nexo 物品的基础。\
这样你可以保留在 MMOItems 中配置的所有内容，并在此基础上添加你自己的机制、纹理、3D 模型等。

```yaml
example_mmoitem:
  itemname: "<gradient:#59A7EA:#F1D2FF>Test"
  mmoitem:
    type: SWORD
    id: FALCON_BLADE
    level: 10 # 可选
    tier: RARE # 可选
    match_level: true # 可选
```

### 在 Nexo 家具 & 自定义方块掉落中使用 MMOItems

你也可以指定在破坏家具或自定义方块时直接掉落某个 MMOItem。
只需在掉落配置中指定 `mmoitems_id` 和 `mmoitems_type`，如下所示：

```yaml
myitemid:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      drop:
        loots:
          - mmoitems_id: FALCON_BLADE
            mmoitems_type: SWORD
            amount: 1..3 # 可选
    furniture:
      drop:
        loots:
          - mmoitems_id: FALCON_BLADE
            mmoitems_type: SWORD
            amount: 1..3 # 可选
```

### 在 Nexo 配方中使用 MMOItems

你还可以在 Nexo 中创建一个配方，使用 MMOItem 作为材料或结果。
与掉落一样，只需指定 `mmoitems_id` 和 `mmoitems_type`。
下面是一个使用 MMOItem 的有序合成配方示例。
如果你在游戏内使用 RecipeBuilders 且该物品是 MMOItem，它也会自动为你生成。

```yaml
myrecipeid:
  result:
    mmoitems_id: FALCON_BLADE
    mmoitems_type: SWORD
  ingredients:
    A:
      mmoitems_id: FALCON_BLADE
      mmoitems_type: SWORD
  shape:
  - ___
  - ___
  - _A_
    
```
