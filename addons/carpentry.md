---
cover: ../.gitbook/assets/image (12).png
coverY: 0
---

# 🚪 木工拓展 (Carpentry)

这是一个 Nexo 的拓展插件，增加了多种新的自定义方块类型。\
它允许你创建自定义的门、活板门、楼梯、台阶以及透明方块。\
下面将展示每种类型的示例。

[Polymart](https://polymart.org/product/7640/carpentry-nexo-addon) | [MCModels](https://mcmodels.net/products/13997/carpentry)

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption><p>Carpentry 默认物品中包含的“灰橡木”木材套装</p></figcaption></figure>

{% hint style="warning" %}
请注意，每种类型目前仅限 4 种变体。
{% endhint %}

### 自定义楼梯

```yaml
custom_stair:
  material: PAPER
  itemname: Custom Stair
  Pack:
    parent_model: block/stairs
    texture: nexo:items/carpentry_blocks/ashen_oak_planks
    #textures:                      # 如果你想使用不同的纹理，可以这样配置
    #  bottom: block/reinforced_deepslate_bottom
    #  side: block/reinforced_deepslate_side
    #  top: block/reinforced_deepslate_top
  Mechanics:
    custom_block:
      type: STAIR
      custom_variation: 1          # 可用范围为 1-4
```

### 自定义台阶

```yaml
custom_slab:
  material: PAPER
  itemname: Custom Slab
  Pack:
    parent_model: block/slab
    texture: nexo:items/carpentry_blocks/ashen_oak_planks
    #textures:                      # 如果你想使用不同的纹理，可以这样配置
    #  bottom: block/reinforced_deepslate_bottom
    #  side: block/reinforced_deepslate_side
    #  top: block/reinforced_deepslate_top
  Mechanics:
    custom_block:
      type: SLAB
      custom_variation: 1          # 可用范围为 1-4
```

### 自定义门

门的设置与其他方块略有不同，因为它需要两个配置文件。
这是因为手持物品的模型如果直接使用方块的父模型会显示不正确。
第二个配置只是为了让 Nexo 生成所需的方块模型。
如果你提供了自己的 json 模型，可以跳过第二个配置。

手持物品的配置：

```yaml
custom_door:
  material: PAPER
  itemname: Custom Door
  Pack:
    parent_model: item/generated   # 手持时使用的模型
    # 手持时显示的物品纹理
    texture: nexo:items/carpentry_blocks/ashen_oak_door_icon
  Mechanics:
    custom_block:
      type: DOOR
      custom_variation: 1          # 可用范围为 1-4
      model: custom_door_placed    # 第二个配置的 itemid，用于生成方块模型
```

放置后方块的配置：

```yaml
custom_door_placed:
  # 生成放置后方块所使用的模型
  # 与其他方块类型的 Pack 配置相同
  # 但因为门的手持物品机制需要拆分
  Pack:
    parent_model: block/door_bottom_left        # 门的默认父模型
    textures:
      bottom: nexo:items/carpentry_blocks/ashen_oak_door_bottom
      top: nexo:items/carpentry_blocks/ashen_oak_door_top
  # 额外属性，防止该物品被注册为 NexoItem
  injectId: false
  excludeFromInventory: true
  excludeFromCommands: true
```

### 自定义活板门

```yaml
custom_trapdoor:
  material: PAPER
  itemname: Custom Trapdoor
  Pack:
    parent_model: block/template_orientable_trapdoor_bottom
    texture: nexo:items/carpentry_blocks/ashen_oak_trapdoor
  Mechanics:
    custom_block:
      type: TRAPDOOR
      custom_variation: 1         # 可用范围为 1-4
```

### 自定义透明方块

这种类型允许创建透明方块，常用于树叶等。
对于普通方块（不需要透明效果），请使用 [音符盒机制](../mechanics/custom-block-mechanics/noteblock-mechanic/)。

```yaml
custom_grate:
  material: PAPER
  itemname: Custom Grate
  Pack:
    parent_model: block/cube_all
    texture: nexo:items/carpentry_blocks/ashen_oak_leaves
  Mechanics:
    custom_block:
      type: GRATE
      custom_variation: 1          # 可用范围为 1-4
```
