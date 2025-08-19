# 基于 Trims (1.20-1.21.1)

如果使用 Trims 作为自定义盔甲类型，大部分内容都会自动处理。
TRIMS 方法需要使用锁链盔甲 (CHAINMAIL) 作为基础物品。

随后 Nexo 会根据你配置的自定义盔甲生成一个数据包。
由于它依赖数据包，因此每次添加/移除盔甲套装时，服务器都需要完全重启。

{% hint style="danger" %}
在将 `CustomArmor.armor_type` 更改为 `TRIMS` 后，你需要：

1. 启动服务器以生成数据包
2. 停止服务器
3. 再次启动服务器以启用先前生成的数据包
   {% endhint %}

## 如何配置你的盔甲？

{% hint style="info" %}
确保你的 NexoItem 的 itemID 遵循 `armorname_armortype` 的模式。
比如下面的套装，其余部分会是 `ruby_chestplate`、`ruby_leggings` 和 `ruby_boots`。

确保你的盔甲层文件遵循 **armorname**\_armor\_layer\_1/2.png 的格式。
在下面的示例中，我们需要 **ruby**\_armor\_layer\_1.png 和 **ruby**\_armor\_layer\_2.png
{% endhint %}

```yaml
ruby_helmet:
  displayname: "<gradient:#FA7CBB:#F14658>Ruby Helmet"
  material: CHAINMAIL_HELMET
  Pack:
    parent_model: "item/generated"
    # 可选，如果未指定，Nexo 会自动查找任何
    # 文件名为 armorname_armor_layer_X.png 的纹理
    #CustomArmor:
    #  layer1: default/armors/ruby_armor_layer_1.png
    #  layer2: default/armors/ruby_armor_layer_2.png
    texture: default/armors/ruby_helmet
```

盔甲正常显示还需要一个修饰图案 (trim-pattern)。
如果没有手动指定，Nexo 会自动分配。
当然，如果你想，也可以手动指定 `trim_pattern`。
其值应为 `nexo:armorname`，在我们的示例中是：

```yaml
ruby_helmet:
  trim_pattern: nexo:ruby
```
