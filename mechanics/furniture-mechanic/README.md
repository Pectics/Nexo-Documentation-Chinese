---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966828778028417125/unknown.png
coverY: 0
---

# 🪑 家具机制

## 家具机制

```yaml
myitem:
  itemname: "<gray>Table"
  material: PAPER
  Pack:
    model: default/table
  Mechanics:
    furniture:
      block_sounds:
        place_sound: block.stone.place
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # 在 Nexo/sounds.yml 中定义的自定义音效
        step_sound: my.custom.stepsound   # 需要在 Nexo/pack 文件夹中提供对应音效文件
        fall_sound: my.custom.fallsound
      hitbox:
        barriers:
          - 0,0,0
      drop:
        silktouch: false
        # 如果没有定义 loots 部分，则掉落自身
        #loots:
        #  - { nexo_item: table, probability: 1.0 }
```

### 家具属性

#### Display Transform

`display_transform` 决定了模型的显示方式。
默认设置为 `NONE`，这会让它的显示效果与在 BlockBench 中打开时一致。
由于某些插件可能会使用盔甲架并将家具附加到头部，你也可以将此选项设置为 `HEAD` 来实现相同的效果。
除此之外还有：`FIRSTPERSON_LEFTHAND`, `FIRSTPERSON_RIGHTHAND`, `FIXED`, `GROUND`, `GUI`, `THIRDPERSON_LEFTHAND`, `THIRDPERSON_RIGHTHAND`。
这些都会在游戏中以 BlockBench 的 Display 标签中对应类型的方式显示。
可以查看 [家具位置](https://github.com/Nexo-MC/Nexo-Documentation/blob/master2/mechanics/furniture-mechanic/broken-reference/README.md) 中 FIXED (物品展示框位置) 的示例。

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        display_transform: NONE
```

#### Tracking Rotation / Billboard

`tracking_rotation` 属性定义了家具是否会“追踪”玩家。
这主要用于广告牌、排行榜等需要玩家能看到的物体，而不是普通家具。
可选值：
`FIXED` - 固定不旋转
`VERTICAL` - 围绕垂直轴旋转
`HORIZONTAL` - 围绕水平轴旋转
`CENTER` - 围绕中心点旋转

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        tracking_rotation: FIXED
```

#### Translation

`translation` 属性允许你对家具模型进行偏移。可以在不修改模型 json 文件的情况下进行视觉调整。
配置如下：

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        translation: 1.0,0,2
```

#### Brightness

`brightness` 属性允许你覆盖家具的原版光照数值。
它有 `block_light` 和 `sky_light` 两个子属性，对应 Minecraft 的两种光照类型。配置如下：

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        brightness:
          block_light: 15
          sky_light: 0
```

#### Scale

`scale` 属性可以用来缩放家具。
它有 `x`、`y` 和 `z` 三个子属性，分别对应各轴缩放。配置如下：

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        scale: 1,1,1
```

`view_range`、`shadow_radius`、`shadow_strength` 顾名思义，无需多解释。

### 自定义音效

家具和自定义方块一样，可以拥有自定义音效。

```yaml
myitem:
  Mechanics:
    furniture:
      block_sounds:
        place_sound: block.stone.place
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # 在 Nexo/sounds.yml 中定义的自定义音效
        step_sound: my.custom.stepsound   # 需要在 Nexo/pack 文件夹中提供对应音效文件
        fall_sound: my.custom.fallsound
```

所有音量和音调默认与 Minecraft 方块一致。
如果你想修改音量或音调，可以使用以下格式。
请注意这两种格式是兼容的。
推荐直接使用默认格式，但如果你需要修改，也可以使用扩展格式。

```yaml
myitem:
  Mechanics:
    furniture:
      block_sounds:
        place:
          sound: block.stone.place
          volume: 1.0
          pitch: 0.2
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # 在 Nexo/sounds.yml 中定义的自定义音效
        step_sound: my.custom.stepsound   # 需要在 Nexo/pack 文件夹中提供对应音效文件
        fall_sound: my.custom.fallsound
```

### 可旋转家具

要让家具可以旋转，只需在物品配置中添加：

```yaml
myitem:
  Mechanics:
    furniture:
      rotatable: true
```

### ModelEngine 家具

要让家具使用 ModelEngine 模型，只需在物品配置中添加：

```yaml
myitem:
  Mechanics:
    furniture:
      modelengine_id: name_of_your_bbmodel_file
```

### 点唱机

让家具能播放音乐唱片和自定义唱片。
你可以调整点唱机的 `volume` 和 `pitch`。
还可以设置 `permission`，如果你只想让特定玩家能使用点唱机。
默认权限为空，意味着任何人都能播放。

```yaml
myitem:
  Mechanics:
    furniture:
      jukebox:
        volume: 1.0
        pitch: 1.0
        permission: "nexo.jukebox.play"
```

### 限制旋转角度

你可以通过 `restricted_rotation` 限制家具的旋转朝向数量。
可设置为 STRICT 或 VERY\_STRICT，分别对应 8 个和 4 个朝向。

```yaml
myitem:
  Mechanics:
    furniture:
      restricted_rotation: VERY_STRICT # 如果未指定，默认值为 STRICT
```

### 限制放置

你可以通过 `limited_placing` 子配置自定义某个自定义方块/家具能放置在哪些方块上。
可以用 `roof`、`floor` 和 `wall` 来控制是否允许在屋顶、地板或墙壁放置。默认值均为 `true`。
`type` 用于指定是否只允许 (ALLOW) 或只禁止 (DENY) 放置在特定方块上。
如果 `type` 为 `ALLOW`，则方块只能放置在指定方块上。
如果 `type` 为 `DENY`，则可以放置在除指定方块外的所有方块上。
还有一个 `radius_limitation` 配置，允许你限制某个家具在一定半径内的数量。

```yaml
myitem:
  Mechanics:
    furniture:
      limited_placing:
        radius_limitation:
          radius: 20
          amount: 10
        roof: false
        floor: true
        wall: false
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

`block_tags` 可在 [此页面](https://minecraft.fandom.com/wiki/Tag#Block_tags) 查看。用于允许/禁止一组方块。
`block_types` 是材料名，用于允许/禁止特定的方块列表。
`nexo_blocks` 是 Nexo 中的自定义方块/家具。
这允许其中所有自定义方块和家具，但家具需要有屏障碰撞箱。

### 储物

这是家具和音符盒机制的一个子机制，可以让你创建自定义储物容器。
本质上就是一个箱子、衣柜或其他储物设备。

可用的类型有：*STORAGE, PERSONAL, ENDERCHEST 和 DISPOSAL*。
**STORAGE** 类似于普通箱子，任何人都能打开并查看内容。
**PERSONAL** 类似自定义末影箱，可以调整行数等。
**ENDERCHEST** 就是原版末影箱，但允许你用自定义方块/家具来访问。
**DISPOSAL** 是一个自定义垃圾桶，物品放进去，关闭时会被删除。

```yaml
myitem:
  Mechanics:
    furniture:
      storage:
        type: STORAGE
        rows: 5                             # 默认值: 6
        title: "<red>My Storage"            # 默认值: "Storage"
        open_sound: entity.shulker.open     # 默认值: entity.chest.open
        close_sound: entity.shulker.close   # 默认值: entity.chest.close
```

### 可注水 (Waterloggable)

你可以让家具在水下放置时变为可注水状态。
这主要适用于家具的屏障碰撞箱。

```yaml
myitem:
  Mechanics:
    furniture:
      waterloggable: true
```

### BlockLocker 支持

你可以通过 [BlockLocker](https://www.spigotmc.org/resources/blocklocker.3268/) 来允许家具的保护。
有效的保护类型有 CONTAINER、DOOR、ATTACHABLE。

```yaml
myitem:
  Mechanics:
    furniture:
      blocklocker:
        can_protect: true
        protection_type: CONTAINER
```
