---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966830020419014666/unknown.png
coverY: 0
---

# 🧵 绊线方块机制 (StringBlock Mechanic)

{% hint style="info" %}
STRINGBLOCK 类型最多允许 **127** 种自定义方块。
每个方块对应一个 `custom_variation`

该自定义方块还有一个特殊点：它有两种不同的碰撞箱状态。
在 `custom_variation` 超过 64 时，碰撞箱会比之前的小。
{% endhint %}

## 它是如何工作的？

这种自定义方块最适合用来制作植物、石块和其他装饰物。
它基于原版绊线方块实现，因此会禁用绊线在原版中的所有行为。

## 如何创建一个绊线方块？

### Nexo 资源包配置

下面是一个配置模型/纹理的示例。
`block/cross` 是原版植物常用的模型，它可以将一张二维纹理转化为一个方块。
如果你需要参考，可以看看游戏中的玫瑰丛。

```yaml
jasmine_flower:
  itemname: "<white>Jasmine Flower"
  material: PAPER
  Pack:
    parent_model: "block/cross"
    texture: custom/flowers/jasmine_flower.png # .png 扩展名不是必须的
```

### 绊线方块机制配置

要使用此机制，你需要告诉 Nexo 使用哪个模型（如果使用自动生成的模型，只需写物品的名称 ID）。
接着需要指定一个未被其他装饰占用的 `custom_variation` 值。
你还可以设置方块的硬度，决定它需要多长时间才能被破坏。
`drop.best_tool` 允许指定最佳工具，例如 PICKAXE 适合小石块。

```yaml
jasmine_flower:
  Mechanics:
    custom_block:
      type: STRINGBLOCK
      custom_variation: 2
      model: jasmine_flower
      hardness: 2
      drop:
        silktouch: false
```

## 次级机制

绊线方块还有一些额外属性。
`placeable_on_water` 允许它像睡莲一样放置在水面上。
`is_tall` 让方块拥有双层碰撞箱，类似于高草丛。
`random_place` 接收一个字符串列表，代表其他绊线机制，放置时会随机生成其中之一。

### 高植物

Nexo 提供了 `is_tall` 属性，让 STRINGBLOCK 占据两个方块空间，类似高草。这需要使用特定的父模型，以及上下两个独立纹理。Nexo 提供了默认的父模型可供使用。
下面是一个使用两张不同 PNG 的示例：

```yaml
plant:
  Pack:
    parent_model: nexo:block/tall_plant
    textures:
      bottom: bottom_texture
      top: top_texture
  Mechanics:
    custom_block:
      type: STRINGBLOCK
      is_tall: true
```

## 树苗 (Sapling)

```yaml
sapling:
  Mechanics:
    custom_block:
      type: STRINGBLOCK
      sapling:
        grows_naturally: true # 如果你希望只能由玩家种植，请改为 false
        natural_growth_time: 6000 # 单位为 tick
        grows_from_bonemeal: true
        bonemeal_growth_speedup: 1250
        grow_sound: block.grass.break
        min_light_level: 4
        requires_water_source: false # 如果你希望它必须在水边生长，请改为 true
        schematic: schemTest # 将要生成的结构
        # 这里也可以使用一个结构列表：
        # schematic:
        # - schem: palmTree1
        #   chance: 0.5
        # - schem: palmTree2
        #   chance: 0.5
        replace_blocks: false
        copy_biomes: false
        copy_entities: false
```

你还可以为生长添加一些随机性，或延长检测间隔。
在 `mechanics.yml` 的 stringblock-mechanic 下调整 `sapling_growth_check_delay`。
该值以 tick 为单位，20 = 1 秒。

## BlockLocker

你可以通过 [BlockLocker](https://www.spigotmc.org/resources/blocklocker.3268/) 为其添加保护。
合法的 `protection_type` 有 CONTAINER、DOOR、ATTACHABLE。

```yaml
Mechanics:
  custom_block:
    type: STRINGBLOCK
    blocklocker:
      can_protect: true
      protection_type: CONTAINER
```

![](https://cdn.discordapp.com/attachments/958524021035647046/961424759718047784/unknown.png)
