---
description: 如何在游戏中添加你自己的方块
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827878706708560/unknown.png
coverY: 0
---

# 🎶 音符盒机制 (NoteBlock Mechanic)

{% hint style="info" %}
NOTEBLOCK 类型最多允许 **1149** 种自定义方块。
每个方块对应一个 `custom_variation`
{% endhint %}

## 如何创建一个简单方块？

### 父模型 (Parent Models)

Nexo 物品的根配置与普通物品相同（例如你可以用钻石等任意材料），并设置一个 itemname 等。
建议不要直接使用方块作为 material，而是使用像 PAPER 这样的材料。
在 Pack 部分，你可以为方块指定自定义模型或纹理。
如果你只有纹理，可以指定一个 `parent_model`，Nexo 会自动为你生成所需文件。
一个标准的 1x1x1 方块通常使用 `"block/cube_all"`。

```yaml
my_block:
  itemname: "My block"
  material: DIAMOND
  Pack:
    parent_model: "block/cube_all"
    texture: my_block_texture.png
```

不同的父模型需要的纹理数量不同。
`block/cube_all` 需要 1 张纹理，`block/cube_column` 需要 2 张，`block/cross` 需要 1 张，`block/orientable` 需要 3 张，`block/orientable_vertical` 需要 2 张。
例如，如果你想用方向性方块机制制作一个木头方块，你应该使用 `block/cube_column`。

所有原版模型可以在 [MCAsset](https://mcasset.cloud/1.21.3/assets/minecraft/models/block) 找到。选择一个适合你使用场景的。
推荐在配置中使用“纹理映射”来处理多纹理设置。

```yaml
my_block:
  itemname: "My block"
  material: DIAMOND
  Pack:
    parent_model: "block/cube_top"
    textures:
      side: my_side_texture.png
      top: my_top_texture.png
```

### 自定义方块机制配置

要使用此机制，你需要告诉 Nexo 使用哪个模型（如果使用自动生成的模型，只需写物品的名称 ID）。
接着需要指定一个未被其他方块占用的 `custom_variation` 值。
合法的 `custom_variation` 范围是 1..1149。

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      model: my_block
      drop:
        silktouch: false 
        minimal_type: STONE
```

### 自定义音效

与自定义方块一样，家具也可以有自定义音效。

```yaml
myitem:
  Mechanics:
    custom_block:
      block_sounds:
        place_sound: block.stone.place
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # 在 Nexo/sounds.yml 中定义的自定义音效
        step_sound: my.custom.stepsound   # 需要在 Nexo/pack 文件夹中放置音频文件
        fall_sound: my.custom.fallsound
```

所有音量和音调值默认与 Minecraft 方块一致。
如果你想修改音量或音调，可以使用以下格式。
请注意这两种格式是兼容的。
推荐直接使用默认设置，但你也可以选择修改。

```yaml
myitem:
  Mechanics:
    custom_block:
      block_sounds:
        place:
          sound: block.stone.place
          volume: 1.0
          pitch: 0.2
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # 在 Nexo/sounds.yml 中定义的自定义音效
        step_sound: my.custom.stepsound   # 需要在 Nexo/pack 文件夹中放置音频文件
        fall_sound: my.custom.fallsound
```

### 自定义破坏速度

你可以使用 hardness 子配置自定义方块的破坏速度以及最佳工具。
`drop.best_tool` 定义了该方块的“推荐工具”，这会进一步影响破坏速度。

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      model: my_block
      hardness: 20 # 这会让方块非常难以破坏
      drop:
        silktouch: false 
        minimal_type: STONE
        best_tool: PICKAXE
```

### 限制放置

你可以通过 `limited_placing` 子配置自定义方块/家具的放置位置。
可以使用 `roof`、`floor` 和 `wall` 控制是否允许放置在屋顶、地板和墙面。默认情况下，全部为 `true`。
`type` 定义是只允许 (ALLOW) 还是只禁止 (DENY) 放置在某些方块上。
如果 `type` 是 `ALLOW`，则只能放置在给定的方块上。
如果 `type` 是 `DENY`，则可以放置在除给定方块以外的所有方块上。

```yaml
amethyst_ore:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      limited_placing:
        roof: true
        floor: true
        wall: true
        type: ALLOW
        block_types:
          - GRASS_BLOCK
          - DIRT
        block_tags:
          - base_stone_nether
        nexo_blocks:
          - chair
          - ruby_ore
```

`block_tags` 可在 [此页面](https://minecraft.fandom.com/wiki/Tag#Block_tags) 中找到。用于允许/禁止一组方块。
`block_types` 是具体的材料名称。用于允许/禁止特定方块。
`nexo_blocks` 是在 Nexo 配置中定义的方块。
这允许包含所有自定义方块和家具，但家具需要屏障碰撞箱。

### 信标基座

你也可以让自定义方块作为信标的基座：

{% code lineNumbers="true" %}
```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      beacon_base_block: true
```
{% endcode %}

{% hint style="info" %}
信标在金字塔中检测到任意音符盒时会“激活”，但只有被标记为 `beacon_base_block` 的音符盒才会真正生效。
这是因为它依赖于一个数据包将音符盒加入指定的 Tag，但它并不支持单独的方块状态。
{% endhint %}

### 抗爆性

你可以通过以下配置让自定义方块具备抗爆性。
如果未指定，默认值为 false。
你也可以在掉落配置中加入 `in_explosion: true`，让方块在爆炸时掉落。

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      blast_resistant: true
      drop:
        loots:
          - nexo_item: my_block
            in_explosion: true
```

### BlockLocker

你可以通过 [BlockLocker](https://www.spigotmc.org/resources/blocklocker.3268/) 为其添加保护。
合法的 `protection_type` 有 CONTAINER、DOOR、ATTACHABLE。

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      blocklocker:
        can_protect: true
        protection_type: CONTAINER
```

### 存储

这是一个家具和音符盒机制的子功能，它允许你制作自定义储物容器。
本质上可以是一个箱子、衣柜或任意你想要的东西。

它有几种类型：*STORAGE, PERSONAL, ENDERCHEST & DISPOSAL*。
**STORAGE** 类似于普通箱子，任何人都能打开并查看内容。
**PERSONAL** 类似于自定义末影箱，可以设置行数等参数。
**ENDERCHEST** 实际上就是末影箱背包，但你可以用自定义方块/家具来访问它。
**DISPOSAL** 是自定义垃圾桶，你可以把物品扔进去，关闭时它们会被删除。\\

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      storage:
        type: STORAGE
        rows: 5                             # 默认值: 6
        title: "<red>My Storage"            # 默认值: "Storage"
        open_sound: entity.shulker.open     # 默认值: entity.chest.open
        close_sound: entity.shulker.close   # 默认值: entity.chest.close
```

### 掉落方块

这是一个模拟沙子和沙砾的子功能。放置时如果下面没有方块，它会掉落。

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      is_falling: true # 默认值为 false
```
