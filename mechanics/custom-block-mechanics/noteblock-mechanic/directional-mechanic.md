---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827878706708560/unknown.png
coverY: 0
---

# 方向性机制 (Directional Mechanic)

### 这是什么？

该机制允许方块在放置时根据朝向改变其纹理，就像原版的木头一样。
共有 3 种方向性方块：`LOG`、`FURNACE` 和 `DROPPER`。
`LOG` 占用 3 个自定义方块变体，`FURNACE` 占用 4 个，`DROPPER` 占用 6 个。

{% hint style="info" %}
每个子方块都可以拥有一个 `model` 属性，Nexo 会根据该属性决定显示的内容。
如果子方块没有 `model` 属性，Nexo 会使用父方块的模型。
{% endhint %}

{% hint style="info" %}
模型会根据放置方向自动旋转。
这意味着你可以重复使用同一个模型，它会根据方向自动旋转。
如果子方块定义了模型，它将不会旋转，从而允许你为不同方向使用不同模型。
{% endhint %}

{% embed url="https://user-images.githubusercontent.com/62521371/167680557-750dac77-b4c4-4804-9513-184d776a012d.mp4" %}

### 配置

### 父方块示例:

```yaml
main_block:
  material: PAPER
  Pack:
    parent_model: block/cube_all
    texture: main_block
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      # 放置时显示的模型，如果未指定，则使用 Pack 中的模型
      # 或者 Nexo 自动生成的模型
      #model: main_block
      custom_variation: 1
      directional:
        # 合法的取值有 LOG、FURNACE 和 DROPPER
        directional_type: LOG
        # LOG
        y_block: main_block_y
        x_block: main_block_x
        z_block: main_block_z
        # FURNACE 和 DROPPER
        north_block: main_block_north
        east_block: main_block_east
        south_block: main_block_south
        west_block: main_block_west
        # DROPPER 还需要这些
        up_block: main_block_up
        down_block: main_block_down
      hardness: 1
      drop:
        minimal_type: WOOD
        best_tools:
          - AXE
        silktouch: false
```

#### LOG 类型示例:

```yaml
# 这里不包含上面父方块的配置
main_block_y:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 1
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义
      
main_block_x:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义

main_block_z:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 3
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义
```

#### FURNACE 类型示例:

```yaml
# 这里不包含上面父方块的配置
main_block_north:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 1
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义
      
main_block_south:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义

main_block_west:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 3
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义

main_block_east:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 4
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义
```

#### DROPPER 类型示例:

```yaml
# 这里不包含上面父方块的配置
main_block_north:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 1
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义
      
main_block_south:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义

main_block_west:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 3
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义

main_block_east:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 4
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义

main_block_up:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      # 当方块朝上或朝下时显示的另一个模型
      #model: mainblockmodel_vertical
      custom_variation: 5
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义

main_block_down:
  excludeFromInventory: true # 让物品栏中只包含基础方块
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      # 当方块朝上或朝下时显示的另一个模型
      #model: mainblockmodel_verticall
      custom_variation: 6
      directional:
        parent_block: main_block # 基础方块，用于掉落物定义
```
