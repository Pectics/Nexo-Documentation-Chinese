# 基于组件 (1.21.2+)

如果使用 COMPONENT 作为你的自定义盔甲类型，那么不会有任何限制，不像 TRIMS 那样。
它的另一个好处是完全不需要基于盔甲物品，如果你愿意甚至可以使用 PAPER。
早期方法的所有缺点现在都不存在了，没有任何限制。

## 如何配置你的盔甲？

{% hint style="info" %}
请确保你的 NexoItem 的 itemID 遵循 `armorname_armortype` 的命名规则。
在上面的套装示例中，其余部分应为 `ruby_chestplate`、`ruby_leggings` 和 `ruby_boots`。

请确保你的盔甲贴图文件遵循 **armorname**\_armor\_layer\_1/2.png 的格式。
在下例中，我们需要 **ruby**\_armor\_layer\_1.png 和 **ruby**\_armor\_layer\_2.png
{% endhint %}

```yaml
ruby_helmet:
  displayname: "<gradient:#FA7CBB:#F14658>Ruby Helmet"
  material: PAPER    # 可以是任意材料，盔甲物品或其他物品
  Pack:
    parent_model: "item/generated"
    # 可选项，如果未指定，Nexo 会自动搜索任意符合 armorname_armor_layer_X.png 文件名的纹理
    #CustomArmor:
    #  layer1: default/armors/ruby_armor_layer_1.png
    #  layer2: default/armors/ruby_armor_layer_2.png
    texture: default/armors/ruby_helmet
```

盔甲正常显示还需要一个可装备组件 (Equippable-Component)。
如果没有手动指定，Nexo 会自动分配。
当然，如果你想，也可以手动指定。
其值应为 `nexo:armorname`，在我们的示例中是：

```yaml
ruby_helmet:
  Components:
    equippable:
      slot: HEAD
      model: nexo:ruby
```

{% hint style="warning" %}
如果你为头盔使用了 3D 模型，请不要指定 Components.equippable.model
{% endhint %}
