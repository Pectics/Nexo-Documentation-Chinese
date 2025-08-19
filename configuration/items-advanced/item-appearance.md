---
description: 如何自定义物品外观？
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966824489490976798/unknown.png
coverY: 0
---

# 特殊物品外观

### 为背包图标与装备/手持设置不同的模型

{% hint style="info" %}
此功能仅适用于 1.21.2+ 的服务端与客户端
{% endhint %}

如果你希望物品在背包中显示为 2D 图标，而当戴在头上或手持时显示为 3D 模型或另一个 2D 图标，你可以通过以下方法实现。  

你需要提供一个 ItemModel，用来指定在不同情况下显示哪个模型。\
以下示例使用 `mymodel_icon` 作为 GUI 的模型，并在其他情况使用“fallback”。\
这种方法可以应用于大多数其他上下文，具体可以参考 [这里](https://minecraft.wiki/w/Items_model_definition#display_context)。\
这并不是一份关于 ItemModels 的详细指南，但你可以用它实现非常复杂的效果。  

```json
{
  "model": {
    "type": "select",
    "property": "display_context",
    "cases": [
      {
        "when": "gui",
        "model": {
          "type": "model",
          "model": "namespace:mymodel_icon" // 在 GUI 中显示的模型
        }
      }
    ],
    "fallback": {
      "type": "model",
      "model": "namespace:mymodel" // 在其他场景中使用的模型
    }
  }
}
```

你可以将此文件放在 `Nexo/pack/assets/namespace/items/mymodel.json` 中。  

然后你可以编写 NexoItem 配置文件来引用这个 ItemModel：  

```yaml
myitem:
  itemname: "My Item"
  Components:
    item_model: namespace:mymodel
```

### 使用阻挡状态的 json 模型（盾牌）

```yaml
myitem:
  Pack:
    model: example_shield.json #json 扩展名不是必需的
    blocking_model: example_shield_blocking.json #json 扩展名不是必需的
```

### 使用拉弓状态的 json 模型（弓）

```yaml
myitem:
  Pack:
    model: default/combat_bow
    pulling_models:
      - default/combat_bow_pulling_0
      - default/combat_bow_pulling_1
      - default/combat_bow_pulling_2
```

如果你只有纹理文件，也可以使用 pulling_textures。  

### 使用 charged_model json 模型（弩）

```yml
myitem:
  Pack:
    model: default/custom_bow
    pulling_models:
      - default/custom_bow_pulling_0
      - default/custom_bow_pulling_1
      - default/custom_bow_pulling_2
    charged_model: default/custom_bow_pulling_2
    firework_model: default/custom_bow_charged #可选
```

如果你只有纹理文件，也可以使用 charged_texture 和 firework_texture。  

### 使用 cast_model json 模型（鱼竿）

```yml
myitem:
  Pack:
    model: default/fishing_rod
    cast_model: default/fishing_rod_cast
```

如果你只有纹理文件，也可以使用 cast_texture。  

### 使用 damaged_model json 模型（不同耐久度等级）

```yml
myitem:
  Pack:
    model: default/diamond_sword
    damaged_models:
      - default/diamond_sword_damaged1
      - default/diamond_sword_damaged2
      - default/diamond_sword_damaged3
```

如果你只有纹理文件，也可以使用 damaged_textures。