# 基于组件 (1.21.2+)

如果使用 COMPONENT 作为你的自定义盔甲类型，那么不会有任何限制，不像 TRIMS 那样。
它的另一个好处是完全不需要基于盔甲物品，如果你愿意甚至可以使用 PAPER。
早期方法的所有缺点现在都不存在了，没有任何限制。

## 如何配置你的盔甲？

{% hint style="info" %}
确保你的 NexoItem 的 itemID 遵循 `armorname_armortype` 的模式。
比如下面的套装，其余的部分会是 `forest_chestplate`、`forest_leggings` 和 `forest_boots`。

确保你的盔甲层文件遵循 **armorname**\_armor\_layer\_1/2.png 的格式。
在下面的示例中，我们需要 **forest**\_armor\_layer\_1.png 和 **forest**\_armor\_layer\_2.png
{% endhint %}

```yaml
forest_helmet:
  material: PAPER    # 可以是任意材料，可以是盔甲物品或其他东西
  Pack:
    # 可选，如果未指定，Nexo 会自动查找任何
    # 文件名为 armorname_armor_layer_X.png 的纹理
    #CustomArmor:
    #  layer1: nexo:item/nexo_armors/forest_armor_layer_1
    #  layer2: nexo:item/nexo_armors/forest_armor_layer_2
    texture: nexo:item/nexo_armors/forest_helmet
```

盔甲正常显示还需要一个可装备组件 (Equippable-Component)。
如果没有手动指定，Nexo 会自动分配。
当然，如果你想，也可以手动指定。
其值应为 `nexo:armorname`，在我们的示例中是：

```yaml
forest_helmet:
  Components:
    equippable:
      slot: HEAD
      model: nexo:forest
```

{% hint style="warning" %}
如果你为头盔使用了 3D 模型，请不要指定 Components.equippable.model
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Nexo 自带的森林盔甲套装（玩家、狼、马和羊驼）</p></figcaption></figure>
