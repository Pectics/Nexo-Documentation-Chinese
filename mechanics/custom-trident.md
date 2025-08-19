# 🔱 自定义三叉戟

Nexo 允许你创建自定义三叉戟及其投射物。
该功能在 1.21.4+ 服务器上效果最佳，但在更低版本中也能正常工作。
三叉戟机制本身相对直观，但也有一些可选属性，主要适用于低版本。

默认情况下，任何使用 TRIDENT 作为材质的物品都会被视为自定义三叉戟。
除非你需要调整属性，否则三叉戟机制并非必需。

### 属性

`thrown_item_model` - 三叉戟投射物所使用的 ItemModel，仅适用于 1.21.4+ 服务器。如果未指定，将默认使用 `Components.item_model`（如果有设置）。

`thrown_item` - 指定用于投射物显示的 NexoItem。如果未指定，默认使用该机制所对应的物品。

`display_transform` - 设置模型应使用的 Transform，主要在未使用单独的 ItemModel 时有用。

`rotation` - 设置投射物的基础偏航/俯仰旋转角度。

`damage` - 三叉戟击中实体时的基础伤害，默认值为 8。

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTAoAxayP9PrBtX9UQ5wa%2Fuploads%2FcMJ3GKLdbXDZofLDSj1A%2F2025-05-06_18-25-55_1.mp4?alt=media&token=8d6ffd64-06d1-4340-aa1f-6d10d5d2e84d" %}
展示森林三叉戟
{% endembed %}

{% tabs fullWidth="true" %}
{% tab title="ItemModel (1.21.4+)" %}
在 1.21.4+ 服务器上，你可以采用两种方法：一种是统一的 ItemModel，另一种是为投掷和持有物品分别设置。

Nexo 内置的森林三叉戟使用了统一的 ItemModel 来控制在不同状态下显示的模型。
这主要用于在手持/图标/投掷时显示不同模型。
就像原版三叉戟，在 GUI 中有 2D 图标，手持时和投掷时的模型也有所不同。
下面是 Nexo 自带的森林三叉戟 ItemModel 示例：

```json
{
  "model": {
      "type": "minecraft:condition",
      "property": "minecraft:using_item",
      "on_false": {
        "type": "minecraft:model",
        "model": "nexo:item/nexo_tools/forest_trident"
      },
      "on_true": {
        "type": "minecraft:model",
        "model": "nexo:item/nexo_tools/forest_trident_throwing"
      }
    }
}
```

这个模型会根据物品是否被使用来切换显示。
该文件放在 `assets/nexo/items/forest_trident.json`，并在 NexoItem 中像下面这样引用：
如上所示，它会链接到两个独立的 JSON 模型：
`assets/nexo/models/item/nexo_tools/forest_trident.json`
`assets/nexo/models/item/nexo_tools/forest_trident_throwing.json`

NexoItem 配置应类似如下：

```yaml
forest_trident:
  itemname: Forest Trident
  material: TRIDENT
  Components:
    item_model: nexo:forest_trident
  Mechanics:
    trident:
      display_transform: HEAD
```

<div><figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>森林三叉戟的默认模型</p></figcaption></figure> <figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>森林三叉戟在“投掷”状态下的模型，带旋转</p></figcaption></figure></div>
{% endtab %}

{% tab title="NexoItem (1.20.4+)" %}
```yaml
forest_trident:
  itemname: Forest Trident
  material: TRIDENT
  Pack:
    model: nexo:item/nexo_tools/forest_trident
  Mechanics:
    trident:
      thrown_item: forest_trident_throwing
      display_transform: HEAD

forest_trident_thrown:
  excludeFromCommands: true
  excludeFromInventory: true
  Pack:
    model: nexo:item/nexo_tools/forest_trident_throwing
```
{% endtab %}
{% endtabs %}
