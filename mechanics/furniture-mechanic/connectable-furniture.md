---
description: Nexo 1.5 中引入的特性
cover: ../../.gitbook/assets/image (11).png
coverY: 0
---

# 🖇️ 可连接家具

Nexo 允许你制作能够相互连接的家具，从而组成不同的视觉效果。
例如，椅子可以拼接成沙发，小桌子可以组合成大桌子。

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Nexo 默认物品中包含的可连接家具</p></figcaption></figure>

#### 连接类型

一个可连接家具由几种不同的变体组成。
上面展示了所有这些的示例。它们用于决定在什么情况下显示哪种模型。
**DEFAULT -** 基础物品，当没有与任何东西连接时放置的形态
**LEFT & RIGHT -** 可连接家具的左右端
**STRAIGHT -** 左端与右端之间的直线部分
**INNER -** 向内的拐角
**OUTER -** 向外的拐角

将该机制添加到家具物品中有几种方式：**ITEM\_MODEL** 和 **ITEM** 类型。

**ITEM\_MODEL** 仅适用于 1.21.2+ 的服务器，但这是推荐方式。
它还允许两种不同的制作方式。
第一种是使用“方块状态 ItemModel”方式。这是推荐方式，因为它减少了资源包中所需的文件数量。

**ITEM** 方式主要适用于 1.20.4 -> 1.21.1 服务器。
它依赖于 NexoItems 来定义连接变体所使用的模型。
最终效果相同，但相比 ITEM\_MODEL，这种方式需要额外的 5 个 NexoItems，从而使配置文件变得更繁琐。

{% tabs fullWidth="true" %}
{% tab title="ITEM\_MODEL (1.21.2+)" %}
ITEM\_MODEL 的工作方式是直接为家具设置要使用的 ItemModel，而不是通过 NexoItem。
这需要你自己提供必要的 ItemModels，但它们非常容易制作。
Nexo 不会自动为你生成这些 ItemModels。

这里也有两种可选方式：Connection-State ItemModel 和普通基础 ItemModels。

BlockState ItemModel 的工作方式是根据物品的属性显示不同的模型。
这意味着你只需要制作一个 ItemModel JSON 文件。

ItemModel 用于修改物品的基础模型，它与 CustomModelData 并不相同。
ItemModel 会链接到一个常规模型，下面展示了在 Nexo 中可用的两种方式的示例。

#### Connection-State ItemModel

它与普通的基础 ItemModel 大体相同，但用作替代大量模型文件。
它通过根据物品上的 "connection-state" 属性选择不同的模型来工作。

下面是一个 ConnectionState ItemModel 的示例，相当直观。
展示给玩家的家具物品会带有一个标记，指定连接状态。
客户端则根据该 ItemModel 来决定使用哪一个模型。
这减少了资源包文件的数量，同时简化了 NexoItem 配置。

该 ItemModel 应放置在例如：`Nexo/pack/assets/nexo/items/connectable/connectable.json`

{% code title="connectable.json" lineNumbers="true" fullWidth="true" %}

```json
{
  "model": {
    "type": "select",
    "property": "block_state",
    "block_state_property": "connectable",
    "cases": [
      {
        "when": "straight",
        "model": {
          "type": "model",
          "model": "nexo:item/nexo_furniture/connectable/connectable_straight"
        }
      },
      {
        "when": "left",
        "model": {
          "type": "model",
          "model": "nexo:item/nexo_furniture/connectable/connectable_left"
        }
      },
      {
        "when": "right",
        "model": {
          "type": "model",
          "model": "nexo:item/nexo_furniture/connectable/connectable_right"
        }
      },
      {
        "when": "inner",
        "model": {
          "type": "model",
          "model": "nexo:item/nexo_furniture/connectable/connectable_inner"
        }
      },
      {
        "when": "outer",
        "model": {
          "type": "model",
          "model": "nexo:item/nexo_furniture/connectable/connectable_outer"
        }
      }
    ],
    "fallback": {
      "type": "model",
      "model": "nexo:item/nexo_furniture/connectable/connectable"
    }
  }
}
```
{% endcode %}

这是使用该 ConnectionState-ItemModel 的 NexoItem 配置。我们无需指定任何子属性。
它将直接使用我们在 Components 部分指定的 ItemModel。

{% code title="connectable\_furniture.yml" %}

```yaml
connectable:
  itemname: Connectable
  Components:
    item_model: nexo:connectable/connectable
  Mechanics:
    furniture:
      connectable:
        type: ITEM_MODEL
      hitbox:
        barriers:
        - 0,0,0
```
{% endcode %}

#### 普通 ItemModel

这种方式需要你为每个连接状态制作一个基础 ItemModel，如下所示：

{% code title="connectable.json" %}
```json
{
  "model": {
    "type": "minecraft:model",
    "model": "nexo:connectable"
  }
}
```
{% endcode %}

现在为六种连接状态都重复这个操作，分别指向不同的模型，并将它们放入资源包中。
例如路径为：`Nexo/pack/assets/nexo/items/connectable/connectable.json`

然后我们只需要制作 NexoItem 配置，并指定它应使用的不同连接状态 ItemModels。

{% code title="connectable\_furniture.yml" %}

```yaml
connectable:
  itemname: Connectable
  Components:
    item_model: nexo:connectable/connectable
  Mechanics:
    furniture:
      connectable:
        type: ITEM_MODEL
        default: nexo:connectable/connectable            # 如果未指定，将使用上方的 ItemModel
        straight: nexo:connectable/connectable_straight  # 如果未指定，将使用 default + "_straight"
        left: nexo:connectable/connectable_left          # 如果未指定，将使用 default + "_left"
        right: nexo:connectable/connectable_right        # 如果未指定，将使用 default + "_right"
        inner: nexo:connectable/connectable_inner        # 如果未指定，将使用 default + "_inner"
        outer: nexo:connectable/connectable_outer        # 如果未指定，将使用 default + "_outer"
      hitbox:
        barriers:
        - 0,0,0
```
{% endcode %}
{% endtab %}

{% tab title="ITEM (<1.21.1)" %}
ITEM 方式依赖 NexoItems 来选择显示的模型。
下面是一个主物品和每个连接状态的子 NexoItems 的配置示例：

```yaml
connectable:
  itemname: Connectable
  Pack:
    model: nexo:items/nexo_furniture/connectable/connectable
  Mechanics:
    furniture:
      connectable:
        type: ITEM
        # 如果未指定 default，将默认使用 ItemID
        default: connectable            # 可以复用该物品，因为我们要使用上面的模型
        straight: connectable_straight  # 如果未指定，将使用 default + "_straight"
        left: connectable_left          # 如果未指定，将使用 default + "_left"
        right: connectable_right        # 如果未指定，将使用 default + "_right"
        inner: connectable_inner        # 如果未指定，将使用 default + "_inner"
        outer: connectable_outer        # 如果未指定，将使用 default + "_outer"
      hitbox:
        barriers:
        - 0,0,0

# 用于链接到模型的虚拟 NexoItems
connectable_straight:
  excludeFromInventory: true
  excludeFromCommands: true
  Pack:
    model: nexo:item/nexo_furniture/connectable/connectable_straight
connectable_left:
  excludeFromInventory: true
  excludeFromCommands: true
  Pack:
    model: nexo:item/nexo_furniture/connectable/connectable_left
connectable_right:
  excludeFromInventory: true
  excludeFromCommands: true
  Pack:
    model: nexo:item/nexo_furniture/connectable/connectable_right
connectable_inner:
  excludeFromInventory: true
  excludeFromCommands: true
  Pack:
    model: nexo:item/nexo_furniture/connectable/connectable_inner
connectable_outer:
  excludeFromInventory: true
  excludeFromCommands: true
  Pack:
    model: nexo:item/nexo_furniture/connectable/connectable_outer
```
{% endtab %}
{% endtabs %}
