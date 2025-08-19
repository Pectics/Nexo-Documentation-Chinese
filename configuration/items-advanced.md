---
description: 关于物品创建的所有细节
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966824770651967498/unknown.png
coverY: 0
---

# ⚒️ 物品

### Components

{% tabs fullWidth="true" %}
{% tab title="1.21.5" %}
`tooltip_display` - 设置要隐藏提示信息的组件。所有 DataComponents 的列表可以在 [这里](https://minecraft.wiki/w/Data_component_format#List_of_components) 找到。请使用它来代替 ItemFlags

`custom_data` - 定义要添加到物品上的自定义属性
`max_stack_size` - 设置 NexoItem 的最大堆叠数量
`enchantment_glint_override` - 设置附魔光效的覆盖状态
`durability` - 设置该 NexoItem 的耐久度
`hide_tooltip` - 悬停时隐藏该 NexoItem 的所有提示信息
`food` - 定义物品作为食物被消耗时的一些专用属性
`consumable` - 使物品可被消耗，包含一系列子属性
`jukebox_playable` - 允许该物品被放入唱片机并播放指定歌曲

* `show_in_tooltip` - 在物品提示中显示歌曲信息
* `song_key` - 歌曲的键值（自定义歌曲需要数据包）

`equippable` - 使该物品可像盔甲一样装备
`damage_resistant` - 指定该物品免疫的伤害类型

* 如果要支持多个伤害类型，需要数据包和新的自定义标签
* 所有可用的伤害类型可在 [这里](https://minecraft.wiki/w/Damage_type_tag_%28Java_Edition%29) 查阅

`enchantable` - 设置该物品在附魔台中的最大附魔消耗
`glider` - 装备后允许玩家滑翔，类似鞘翅
`item_model` - 该物品的基础模型，可替代 custom\_model\_data

* 引用路径：`assets/<namespace>/items/<model>` -> `item_model: namespace:model`

`tooltip_style` - 物品提示框的样式

* 引用自定义的背景精灵：`assets/<namespace>/textures/gui/sprites/tooltip/<id>_background`
* 引用自定义的边框精灵：`assets/<namespace>/textures/gui/sprites/tooltip/<id>_frame`
* 可以通过 mcmeta 自定义和动画化 [Wiki](https://minecraft.wiki/w/Resource_pack#Animation#Gui)

`use_cooldown` - 使用时为所有匹配的物品应用冷却
`use_remainder` - 使用后若堆叠数量减少，将物品替换为余留物
`damage_resistant` - 指定伤害类型的标签键
`repairable` - 指定哪些物品可以在铁砧中修复耐久度
`death_protection` - 当装备时保护玩家免于死亡，可选地附加效果
`custom_model_data` - 用于 [1.21.4 CMD 组件](https://minecraft.wiki/w/Data_component_format#custom_model_data) 的新格式

以上属性的示例：

{% code fullWidth="true" %}
```yaml
my_item:
  itemname: <gradient:#4B36B1:#6699FF>My Item
  Components:
    custom_data:
      nexo:string: "Some string"
      nexo:integer: 2
      nexi:integer_list: [1, 2, 3]
      nexo:string_list: ["something", "something else"]
      nexo:compound:
        nexo:c_string: "Compound String"
        nexo:c_integer: 3
        namespace:boolean: true
    tooltip_display:          # 应当代替 ItemFlags 使用
      - minecraft:enchantments
      - minecraft:attribute_modifiers
    hide_tooltip: true        # 如果为 true，则在悬停时隐藏整个提示框
    enchantment_glint_override: false
    durability: 10
    # 如果上方的材料不是正常工具，而是 PAPER 之类
    # 那么物品默认不会因动作而降低耐久度
    # 示例：让该工具在攻击实体或破坏方块时损耗耐久度
    #durability:
    #  value: 10
    #  damage_block_break: true
    #  damage_entity_hit: true
    max_stack_size: 10
    tool:
      #damage_per_block:                      # 可选，默认值为 1
      #default_mining_speed:                  # 可选，默认值为 1.0
      rules:
        - speed: 1.0
          correct_for_drops: true             # 挖掘给定方块时是否掉落
          material: DIAMOND_BLOCK             # 此规则适用的方块材料，也支持列表格式
          #materials:
          #  - DIAMOND_BLOCK
          #  - NETHERITE_BLOCK
          # 所有标签列表可在 https://minecraft.wiki/w/Tag#Block_tags_2 查阅
          tag: minecraft:mineable/axe         # 此规则适用的方块标签，也支持列表格式
          #tags:
          #  - minecraft:mineable/axe
          #  - minecraft:mineable/shovel
    food:
      nutrition: 2
      saturation: 2 
      #can_always_eat: false                  # 可选，默认值为 false
    consumable:
      sound: minecraft:entity.generic.eat     # 可选，默认值为 entity.generic.eat
      consume_particles: true                 # 可选，默认值为 true
      consume_seconds: 1.6                    # 可选，默认值为 1.6
      animation: EAT                          # 可选，默认值为 EAT
      effects:
        APPLY_EFFECTS:
          mining_fatigue:
            duration: 10
            amplifier: 1
            ambient: false
            show_icon: true
            show_particles: true
            probability: 1.0
        REMOVE_EFFECTS:
        - speed
        CLEAR_ALL_EFFECTS: {}
        TELEPORT_RANDOMLY:
          diameter: 16.0
        PLAY_SOUND:
          sound: minecraft:ambient.basalt_deltas.additions1
    damage_resistant: is_fire
    enchantable: 1
    glider: true
    item_model: minecraft:example         #`assets/minecraft/models/item/example.json`
    tooltip_style: minecraft:example      #`assets/minecraft/textures/gui/sprites/tooltip/example_(background & frame)`
    use_remainder:
      #minecraft_type: DIAMOND
      #crucible_item: crucibleid
      #eco_item: ecoid
      #mmoitems_id: id
      #mmoitems_type: type
      nexo_item: itemid
    use_cooldown:
      seconds: 1.2                        # 默认值为 1.0
      group: nexo:example                 # 默认值为 `nexo:itemid`，设为空字符串则按材料分类
    damage_resistant: minecraft:is_fire   # 用于替代 1.21 的 isFireResistant
    repairable: minecraft:planks          # 支持单个字符串或字符串列表
      #- minecraft:diamond                # 支持单个材料或标签
    equippable:
      slot: HEAD
      #model: minecraft:example           可选，主要用于自定义盔甲
      #camera_overlay: minecraft:example  可选，例如 carved_pumpkin，示例路径：`assets/minecraft/textures/example.png`
      #equip_sound: item.armor.equip_chain
      #allowed_entity_types:              可选，默认允许所有实体
      #  - PLAYER
      #  - SKELETON
      #dispensable: true                  可选，默认值为 true
      #swappable: true                    可选，默认值为 true
      #damage_on_hurt: true               可选，默认值为 true
    death_protection:
      death_effects:                      # 可选，可以为空或设为 []
        APPLY_EFFECTS:
          mining_fatigue:
            duration: 10
            amplifier: 1
            ambient: false
            show_icon: true
            show_particles: true
            probability: 1.0
          REMOVE_EFFECTS:
          - speed
          CLEAR_ALL_EFFECTS: {}
          TELEPORT_RANDOMLY:
            diameter: 16.0
          PLAY_SOUND:
            sound: minecraft:ambient.basalt_deltas.additions1
    custom_model_data:                  # 更详细的说明见：https://minecraft.wiki/w/Data_component_format#custom_model_data
      #floats: [ 1f, 2f, ...]           # 可选，与之前 CMD 相同逻辑
      #colors: [ 1, 123456, [r, g, b]]
      #string: [ "something", "somethingelse", ...]
      #flags: []
```
{% endcode %}
{% endtab %}

{% tab title="1.21.4" %}
`custom_data` - 定义要添加到物品的自定义属性
`max_stack_size` - 设置 NexoItem 的最大堆叠数量
`enchantment_glint_override` - 设置附魔光效的覆盖状态
`durability` - 设置此 NexoItem 的耐久度
`hide_tooltip` - 在鼠标悬停时隐藏该 NexoItem 的所有提示信息
`food` - 定义与食物相关的部分属性，在物品被食用时生效
`consumable` - 让物品可消耗，并包含一系列子属性
`jukebox_playable` - 允许此物品放入唱片机并播放指定的歌曲

* `show_in_tooltip` - 在物品提示中显示歌曲信息
* `song_key` - 歌曲的键值（自定义歌曲需要数据包）

`equippable` - 让此物品可像盔甲一样装备
`damage_resistant` - 指定此物品对某类伤害免疫

* 如果你想支持多种伤害类型，需要一个包含自定义标签的数据包
* 所有可用的伤害类型可在 [这里](https://minecraft.wiki/w/Damage_type_tag_%28Java_Edition%29) 找到

`enchantable` - 设置此物品在附魔台中的最大附魔消耗
`glider` - 当装备时允许玩家像鞘翅一样滑翔
`item_model` - 此物品的基础模型，可替代 custom\_model\_data

* 引用路径为 `assets/<namespace>/items/<model>` -> `item_model: namespace:model`

`tooltip_style` - 物品提示信息的样式

* 引用自定义的精灵背景 `assets/<namespace>/textures/gui/sprites/tooltip/<id>_background`
* 引用自定义的精灵边框 `assets/<namespace>/textures/gui/sprites/tooltip/<id>_frame`
* 可以通过 mcmeta 文件自定义和制作动画 [Wiki](https://minecraft.wiki/w/Resource_pack#Animation#Gui)

`use_cooldown` - 使用时对所有匹配物品施加冷却
`use_remainder` - 如果物品堆叠数量在使用后减少，则用剩余物品替换
`damage_resistant` - 指定伤害类型的标签键
`repairable` - 指定哪些物品可用于铁砧中修复耐久度
`death_protection` - 当装备时保护玩家免于死亡，也可选择性地施加效果
`custom_model_data` - 用于 [1.21.4 CMD 组件](https://minecraft.wiki/w/Data_component_format#custom_model_data) 的新格式化支持

以上属性的示例：

{% code fullWidth="true" %}
```yaml
my_item:
  itemname: <gradient:#4B36B1:#6699FF>My Item
  Components:
    custom_data:
      nexo:string: "Some string"
      nexo:integer: 2
      nexi:integer_list: [1, 2, 3]
      nexo:string_list: ["something", "something else"]
      nexo:compound:
        nexo:c_string: "Compound String"
        nexo:c_integer: 3
        namespace:boolean: true
    enchantment_glint_override: false
    durability: 10
    # 如果上面的 material 不是常规工具，而是像 PAPER 这样的材质
    # 默认情况下，该物品不会因为操作而损失耐久
    # 下面的例子展示了如何让工具在击打实体或破坏方块时损耗耐久
    #durability:
    #  value: 10
    #  damage_block_break: true
    #  damage_entity_hit: true
    max_stack_size: 10
    hide_tooltip: true
    tool:
      #damage_per_block:                      # 可选，默认值为 1
      #default_mining_speed:                  # 可选，默认值为 1.0
      rules:
        - speed: 1.0
          correct_for_drops: true             # 是否在挖掘指定方块时掉落物品
          material: DIAMOND_BLOCK             # 此规则应用的方块材质，也支持列表格式
          #materials:
          #  - DIAMOND_BLOCK
          #  - NETHERITE_BLOCK
          # 所有方块标签可在 https://minecraft.wiki/w/Tag#Block_tags_2 找到
          tag: minecraft:mineable/axe         # 此规则应用的方块标签，也支持列表格式
          #tags:
          #  - minecraft:mineable/axe
          #  - minecraft:mineable/shovel
    food:
      nutrition: 2
      saturation: 2 
      #can_always_eat: false                  # 可选，默认为 false
    consumable:
      sound: minecraft:entity.generic.eat     # 可选，默认值为 entity.generic.eat
      consume_particles: true                 # 可选，默认值为 true
      consume_seconds: 1.6                    # 可选，默认值为 1.6
      animation: EAT                          # 可选，默认值为 EAT
      effects:
        APPLY_EFFECTS:
          mining_fatigue:
            duration: 10
            amplifier: 1
            ambient: false
            show_icon: true
            show_particles: true
            probability: 1.0
        REMOVE_EFFECTS:
        - speed
        CLEAR_ALL_EFFECTS: {}
        TELEPORT_RANDOMLY:
          diameter: 16.0
        PLAY_SOUND:
          sound: minecraft:ambient.basalt_deltas.additions1
    damage_resistant: is_fire
    enchantable: 1
    glider: true
    item_model: minecraft:example         #`assets/minecraft/models/item/example.json`
    tooltip_style: minecraft:example      #`assets/minecraft/textures/gui/sprites/tooltip/example_(background & frame)`
    use_remainder:
      #minecraft_type: DIAMOND
      #crucible_item: crucibleid
      #eco_item: ecoid
      #mmoitems_id: id
      #mmoitems_type: type
      nexo_item: itemid
    use_cooldown:
      seconds: 1.2                        # 默认值为 1.0
      group: nexo:example                 # 默认值为 `nexo:itemid`，设置为 ""（空值）则按材质生效
    damage_resistant: minecraft:is_fire   # 替代 1.21 中的 isFireResistant
    repairable: minecraft:planks          # 支持单个字符串或字符串列表
      #- minecraft:diamond                # 同时支持单个材质和标签
    equippable:
      slot: HEAD
      #model: minecraft:example           可选，主要用于自定义盔甲
      #camera_overlay: minecraft:example  可选，用于南瓜头等，例：`assets/minecraft/textures/example.png`
      #equip_sound: item.armor.equip_chain
      #allowed_entity_types:              可选，默认支持所有实体
      #  - PLAYER
      #  - SKELETON
      #dispensable: true                  可选，默认值为 true
      #swappable: true                    可选，默认值为 true
      #damage_on_hurt: true               可选，默认值为 true
    death_protection:
      death_effects:                      # 可选，可以为空或设为 []
        APPLY_EFFECTS:
          mining_fatigue:
            duration: 10
            amplifier: 1
            ambient: false
            show_icon: true
            show_particles: true
            probability: 1.0
          REMOVE_EFFECTS:
          - speed
          CLEAR_ALL_EFFECTS: {}
          TELEPORT_RANDOMLY:
            diameter: 16.0
          PLAY_SOUND:
            sound: minecraft:ambient.basalt_deltas.additions1
    custom_model_data:                   # 深入说明见：https://minecraft.wiki/w/Data_component_format#custom_model_data
      #floats: [ 1f, 2f, ...]            # 可选，与之前的 CMD 逻辑相同
      #colors: [ 1, 123456, [r, g, b]]
      #string: [ "something", "somethingelse", ...]
      #flags: []
```
{% endcode %}
{% endtab %}

{% tab title="1.21.3" %}
`custom_data` - 定义要添加到物品的自定义属性
`max_stack_size` - 设置 NexoItem 的最大堆叠数量
`enchantment_glint_override` - 设置物品附魔光效的覆盖状态
`durability` - 设置此 NexoItem 的耐久度
`hide_tooltip` - 当鼠标悬停时隐藏该 NexoItem 的所有提示信息
`food` - 定义物品作为食物时的一些属性
`consumable` - 使物品可被消耗，并包含多个子属性
`jukebox_playable` - 允许此物品被放入唱片机中播放指定的歌曲

* `show_in_tooltip` - 在物品提示中显示歌曲信息
* `song_key` - 歌曲的键值（自定义歌曲需要数据包）

`equippable` - 使物品可像盔甲一样被装备
`damage_resistant` - 指定此物品对某种伤害类型免疫

* 如果你想支持多种伤害类型，需要一个包含自定义标签的数据包
* 所有可用的伤害类型可以在 [这里](https://minecraft.wiki/w/Damage_type_tag_%28Java_Edition%29) 查看

`enchantable` - 设置此物品在附魔台中的最大附魔消耗
`glider` - 当装备时允许玩家像鞘翅一样滑翔
`item_model` - 此物品的基础模型，可替代 custom\_model\_data

* 引用路径为 `assets/<namespace>/models/item/<model>` -> `item_model: namespace:model`

`tooltip_style` - 物品提示信息的样式

* 自定义提示背景引用路径：`assets/<namespace>/textures/gui/sprites/tooltip/<id>_background`
* 自定义提示边框引用路径：`assets/<namespace>/textures/gui/sprites/tooltip/<id>_frame`
* 可以通过 mcmeta 文件自定义和设置动画 [Wiki](https://minecraft.wiki/w/Resource_pack#Animation#Gui)

`use_cooldown` - 为所有符合条件的物品使用时应用冷却
`use_remainder` - 如果物品在使用后堆叠数减少，则替换为剩余物品
`damage_resistant` - 对应伤害类型的标签键值
`repairable` - 指定哪些物品可以在铁砧中用于修复耐久度
`death_protection` - 当装备时在玩家死亡时保护玩家，可选地附带效果

以上属性示例：

{% code fullWidth="true" %}
```yaml
my_item:
  itemname: <gradient:#4B36B1:#6699FF>My Item
  Components:
    custom_data:
      nexo:string: "Some string"
      nexo:integer: 2
      nexi:integer_list: [1, 2, 3]
      nexo:string_list: ["something", "something else"]
      nexo:compound:
        nexo:c_string: "复合字符串"
        nexo:c_integer: 3
        namespace:boolean: true
    enchantment_glint_override: false
    durability: 10
    # 如果上面的 material 不是常规工具，例如 PAPER
    # 默认情况下，物品不会因为操作而降低耐久度
    # 下面是一个示例：让工具在攻击实体和破坏方块时降低耐久度
    #durability:
    #  value: 10
    #  damage_block_break: true
    #  damage_entity_hit: true
    max_stack_size: 10
    hide_tooltip: true
    tool:
      #damage_per_block:                       # 可选，默认为 1
      #default_mining_speed:                   # 可选，默认为 1.0
      rules:
        - speed: 1.0
          correct_for_drops: true             # 挖掘这些方块时是否掉落
          material: DIAMOND_BLOCK             # 规则适用的方块材质，也支持列表格式
          #materials:
          #  - DIAMOND_BLOCK
          #  - NETHERITE_BLOCK
          # 所有标签列表可见：https://minecraft.wiki/w/Tag#Block_tags_2
          tag: minecraft:mineable/axe         # 规则适用的方块标签，也支持列表格式
          #tags:
          #  - minecraft:mineable/axe
          #  - minecraft:mineable/shovel
    food:
      nutrition: 2
      saturation: 2 
      #can_always_eat: false                   # 可选，默认值为 false
    consumable:
      sound: minecraft:entity.generic.eat     # 可选，默认值 entity.generic.eat
      consume_particles: true                 # 可选，默认值 true
      consume_seconds: 1.6                    # 可选，默认值 1.6
      animation: EAT                          # 可选，默认值 EAT
      effects:
        APPLY_EFFECTS:
          mining_fatigue:
            duration: 10
            amplifier: 1
            ambient: false
            show_icon: true
            show_particles: true
            probability: 1.0
        REMOVE_EFFECTS:
        - speed
        CLEAR_ALL_EFFECTS: {}
        TELEPORT_RANDOMLY:
          diameter: 16.0
        PLAY_SOUND:
          sound: minecraft:ambient.basalt_deltas.additions1
    damage_resistant: is_fire
    enchantable: 1
    glider: true
    item_model: minecraft:example         #`assets/minecraft/models/item/example.json`
    tooltip_style: minecraft:example      #`assets/minecraft/textures/gui/sprites/tooltip/example_(background & frame)`
    use_remainder:
      #minecraft_type: DIAMOND
      #crucible_item: crucibleid
      #eco_item: ecoid
      #mmoitems_id: id
      #mmoitems_type: type
      nexo_item: itemid
    use_cooldown:
      seconds: 1.2                        # 默认值 1.0
      group: nexo:example                 # 默认值 `nexo:itemid`，设为 "" 空字符串则按材质生效
    damage_resistant: minecraft:is_fire   # 替代 1.21 的 isFireResistant
    repairable: minecraft:planks          # 支持单个字符串或字符串列表
      #- minecraft:diamond                # 同时支持单个材质和标签
    equippable:
      slot: HEAD
      #model: minecraft:example           # 可选，主要用于自定义盔甲
      #camera_overlay: minecraft:example  # 可选，用于雕刻南瓜等，示例：`assets/minecraft/textures/example.png`
      #equip_sound: item.armor.equip_chain
      #allowed_entity_types:              # 可选，默认支持所有实体
      #  - PLAYER
      #  - SKELETON
      #dispensable: true                  # 可选，默认值 true
      #swappable: true                    # 可选，默认值 true
      #damage_on_hurt: true               # 可选，默认值 true
    death_protection:
      death_effects:                      # 可选，可以为空或 []
        APPLY_EFFECTS:
          mining_fatigue:
            duration: 10
            amplifier: 1
            ambient: false
            show_icon: true
            show_particles: true
            probability: 1.0
          REMOVE_EFFECTS:
          - speed
          CLEAR_ALL_EFFECTS: {}
          TELEPORT_RANDOMLY:
            diameter: 16.0
          PLA
            sound: minecraft:ambient.basalt_deltas.additions1custom_data - 定义要添加到物品的自定义属性
 
max_stack_size - 设置 NexoItem 的最大堆叠数量
enchantment_glint_override - 设置物品附魔光效的覆盖状态
fire_resistant - 设置该 NexoItem 是否免疫火焰和岩浆
durability - 设置此 NexoItem 的耐久度
hide_tooltip - 当鼠标悬停时隐藏该 NexoItem 的所有提示信息
food - 使物品可食用，带有多个不同属性
jukebox_playable - 允许此物品被放入唱片机并播放指定歌曲
```
{% endcode %}
{% endtab %}

{% tab title="1.21.1" %}
`custom_data` - 定义要添加到物品上的自定义属性
`max_stack_size` - 设置 NexoItem 的最大堆叠数量
`enchantment_glint_override` - 设置物品附魔光效的覆盖状态
`fire_resistant` - 设置该 NexoItem 是否对火焰和岩浆免疫
`durability` - 设置该 NexoItem 的耐久度
`hide_tooltip` - 悬停时隐藏该 NexoItem 的所有提示信息
`food` - 让该物品可被食用，并带有多个不同的属性
`jukebox_playable` - 允许该物品被放入唱片机并播放指定的歌曲

* `show_in_tooltip` - 在物品提示中显示歌曲信息
* `song_key` - 歌曲的键值（自定义歌曲需要数据包）

上述所有属性的示例：

```yaml
my_item:
  itemname: <gradient:#4B36B1:#6699FF>My Item
  Components:
    custom_data:
      nexo:string: "Some string"
      nexo:integer: 2
      nexi:integer_list: [1, 2, 3]
      nexo:string_list: ["something", "something else"]
      nexo:compound:
        nexo:c_string: "复合字符串"
        nexo:c_integer: 3
        namespace:boolean: true
    enchantment_glint_override: false
    durability: 10
    # 如果上面的材质不是常规工具，比如 PAPER
    # 该物品不会因为使用行为而降低耐久
    # 例如：让工具因攻击实体或破坏方块而降低耐久
    #durability:
    #  value: 10
    #  damage_block_break: true
    #  damage_entity_hit: true
    max_stack_size: 10
    fire_resistant: true
    hide_tooltip: true
    tool:
      damage_per_block:                       # 可选，默认值为 1
      default_mining_speed:                   # 可选，默认值为 1.0
      rules:
        - speed: 1.0
          correct_for_drops: true             # 挖掘对应方块时是否会掉落
          material: DIAMOND_BLOCK             # 规则适用的方块材质，也支持列表格式
          #materials:
          #  - DIAMOND_BLOCK
          #  - NETHERITE_BLOCK
          # 所有可用标签请参考 https://minecraft.wiki/w/Tag#Block_tags_2
          tag: minecraft:mineable/axe         # 规则适用的方块标签，也支持列表格式
          #tags:
          #  - minecraft:mineable/axe
          #  - minecraft:mineable/shovel
    food:
      nutrition: 2
      saturation: 2 
      can_always_eat: false                   # 可选，默认值为 false
      eat_seconds: 1.6                        # 可选，默认值为 1.6
      replacement:                            # 可选，仅限 1.21+，若未指定则为 null（即无替换物）
        #minecraft_type: DIAMOND
        #crucible_item: crucibleid
        #eco_item: ecoid
        #mmoitems_id: id
        #mmoitems_type: type
        nexo_item: itemid
      effects:
        mining_fatigue:
          duration: 10                        # 持续时间（秒），默认值为 20
          amplifier: 1
          ambient: false
          show_icon: true
          show_particles: true
          probability: 0.5                    # 0.5 = 50%
      jukebox_playable:
        show_in_tooltip: true
        song_key: mysong.id
```
{% endtab %}

{% tab title="1.20.5" %}
`max_stack_size` - 设置 NexoItem 的最大堆叠数量
`enchantment_glint_override` - 设置附魔光效的覆盖状态
`fire_resistant` - 设置该 NexoItem 是否对火焰和岩浆免疫
`durability` - 设置该 NexoItem 的耐久度
`hide_tooltip` - 在悬停时隐藏该 NexoItem 的所有提示信息
`food` - 使该物品可食用，并带有多种属性

以上所有属性的示例：

```yaml
my_item:
  itemname: <gradient:#4B36B1:#6699FF>My Item
  Components:
    enchantment_glint_override: false
    durability: 10
    # 如果上面的材质不是普通工具，比如 PAPER
    # 物品在默认情况下不会因为操作而损失耐久
    # 例如让该工具因攻击实体或破坏方块而降低耐久
    #durability:
    #  value: 10
    #  damage_block_break: true
    #  damage_entity_hit: true
    max_stack_size: 10
    fire_resistant: true
    hide_tooltip: true
    tool:
      damage_per_block:                       # 可选，默认为 1
      default_mining_speed:                   # 可选，默认为 1.0
      rules:
        - speed: 1.0
          correct_for_drops: true             # 挖掘指定方块时是否掉落
          material: DIAMOND_BLOCK             # 该规则适用的方块材质，也支持列表格式
          #materials:
          #  - DIAMOND_BLOCK
          #  - NETHERITE_BLOCK
          # 所有标签列表见 https://minecraft.wiki/w/Tag#Block_tags_2
          tag: minecraft:mineable/axe         # 该规则适用的方块标签，也支持列表格式
          #tags:
          #  - minecraft:mineable/axe
          #  - minecraft:mineable/shovel
    food:
      nutrition: 2
      saturation: 2 
      can_always_eat: false                   # 可选，默认为 false
      eat_seconds: 1.6                        # 可选，默认为 1.6
      replacement:                            # 可选，仅 1.21+，未指定时为 null（即没有替代物）
        #minecraft_type: DIAMOND
        #crucible_item: crucibleid
        #eco_item: ecoid
        #mmoitems_id: id
        #mmoitems_type: type
        nexo_item: itemid
      effects:
        mining_fatigue:
          duration: 10                        # 单位秒，默认值为 20
          amplifier: 1
          ambient: false
          show_icon: true
          show_particles: true
          probability: 0.5                    # 0.5 = 50%
```
{% endtab %}
{% endtabs %}

### ItemTemplate

这允许你轻松地将一个模板物品的属性复制到其他物品上。
在你想要继承属性的物品中，只需指定模板物品的 ItemID。
它也支持多个物品的列表，从而将多个物品的属性合并到一个物品中。

```yml
template_item:
  itemname: Template Item
  material: DIAMOND

template_item1:
  template: template_item
  itemname: Template Item 1

template_item2:
  templates: 
    - template_item
    - template_item1
```

### PersistentData

这允许你将自定义数据添加到物品的 PersistentDataContainer 中。它们存储在物品的 `PublicBukkitValues` 中。type 表示要添加的数据类型。支持的数据类型可以在 [这里](https://jd.papermc.io/paper/1.21.5/org/bukkit/persistence/PersistentDataType.html#field-summary) 找到。Nexo 还提供了一些自定义的数据类型，例如 UUID，可以在 [这里](https://hub.jeff-media.com/javadocs/morepersistentdatatypes/) 找到。

```yaml
myitem:
  PersistentData:
    - type: STRING
      key: mynamespace:something
      value: "Hi this is a string"
```

### Itemname

这允许你更改物品的显示名称，而不会影响被重命名过的物品。

```yaml
my_item:
  itemname: "<red><bold>Example"
```

### Displayname

这只在 1.20.4 版本中有用，更高版本将直接使用 Itemname。
`custom_name` 会设置物品的显示名/自定义名，如果你需要使用这个旧版特性。

```yaml
my_item:
  displayname: "<red><bold>Example"
  #customname: "<red><bold>Example"
```

### Material

这允许你更改物品的类型。

```yaml
my_item:
  material: WOODEN_SWORD
```

### Color

这允许你更改由支持材质（如皮革盔甲）制成的物品的颜色。

{% columns %}
{% column width="58.333333333333336%" %}
```yaml
my_item:
  color: 3, 252, 136 #rgb
```

要更改模型的颜色，你需要设置 Tint 属性。
在 BlockBench 中设置 `Tint` 属性的方法：

* 在 BlockBench 中打开模型
* 打开“涂装”面板
* 选择你想要改变颜色的面
* 右键点击该面并勾选 `Tint` 选项
{% endcolumn %}

{% column width="41.666666666666664%" %}
![](../.gitbook/assets/tint.png)
{% endcolumn %}
{% endcolumns %}

### Lore

这允许你在物品名称下方添加多行文本说明。

```yaml
my_item:
  lore:
  - "One line"
  - "<green>Another line"
```

### Disable Enchanting

此选项允许你阻止物品通过铁砧或附魔台进行附魔。\
这并不会阻止在配置文件中直接添加附魔。\\

```yaml
my_item:
  disable_enchanting: true
```

{% hint style="warning" %}
从 1.21.2+ 开始，你应该使用 **Enchantable-Component**（`Components.enchantable: 0`）。
{% endhint %}

### excludeFromInventory

此选项允许你将物品从 Nexo 的物品库中排除。它将不会显示，但你仍可以通过 [nexo give 命令](../general-usage/commands.md#get-the-items) 获取它。这在物品用于其他插件（如背包图标）时非常有用。

```yaml
my_item:  
  excludeFromInventory: true
```

### unbreakable

```yaml
my_item:
  unbreakable: true
```

### ItemFlags

这允许你为物品设置 ItemFlags，可用的标志列表可在 [这里](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/inventory/ItemFlag.html) 找到。

```yaml
my_item:
  ItemFlags:
    - HIDE_ENCHANTS
    - HIDE_ATTRIBUTES
    - HIDE_UNBREAKABLE
    - HIDE_DESTROYS
    - HIDE_PLACED_ON
    - HIDE_POTION_EFFECTS
```

### PotionEffects

这允许你为药水添加自定义的药水效果。可用效果的列表在 [这里](https://jd.papermc.io/paper/1.21.3/org/bukkit/potion/PotionEffectType.html) 找到。

```yaml
my_item:
  PotionEffects:
    # - type: 在这里获取效果列表: https://jd.papermc.io/paper/1.21.3/org/bukkit/potion/PotionEffectType.html
    # - duration: 持续时间（以刻为单位）
    # - amplifier: 药水效果等级
    # - ambient: true/false，是否产生更轻、更透明的粒子
    # - particles: true/false，是否显示粒子效果
    # - icon: true/false，是否显示药水图标
    - type: WITHER
      duration: 200
      amplifier: 2
      ambient: false
      particles: true
      icon: true
```

### AttributeModifiers

这允许你为物品添加 Minecraft 属性。它们非常强大，可以让物品增加生命值、提升玩家速度等。可用属性的列表在 [这里](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/attribute/Attribute.html) 找到。

```yaml
my_item:
  AttributeModifiers:
    # - attribute: 属性，列表见 https://hub.spigotmc.org/javadocs/spigot/org/bukkit/attribute/Attribute.html
    # - operations: 0 表示 ADD_NUMBER，1 表示 ADD_SCALAR，2 表示 MULTIPLY_SCALAR_1
    # - slot: HAND, OFF_HAND, FEET, LEGS, CHEST 或 HEAD
    - attribute: GENERIC_MOVEMENT_SPEED
      amount: 0.1 
      operation: 0
      slot: HAND
```

### Enchantments

如果你想为物品添加附魔（即使是非原版等级，比如锋利 15），你可以在这一部分进行配置。

```yaml
my_item:
  Enchantments:
    protection: 4
    flame: 34
    sharpness: 18
```

### 如何设置特定的 CustomModelData？

```yaml
my_item:
  Pack:
    parent_model: "custom/items/generated_elite"
    texture: custom/items/elite_zombie_walk
    custom_model_data: 452
```

## Pack 选项

这部分有专门的页面，你可以在 [这里](items-advanced/item-appearance.md) 查阅。

## Mechanics 选项

这部分有专门的页面，你可以在 [这里](broken-reference/) 查阅。
