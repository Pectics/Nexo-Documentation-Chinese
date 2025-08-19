---
cover: ../../.gitbook/assets/image (1) (1) (1) (1).png
coverY: 0
---

# 🪽 自定义鞘翅 (1.21.2+)

这是基于 COMPONENT 自定义盔甲的一个子功能，允许你制作自定义纹理的鞘翅。
添加它的规则与 [自定义盔甲](components.md) 部分所述完全相同，只是有一些细微区别。Equippable-Component 的 model 属性需要加上后缀 \_elytra，而 itemid 遵循 `armorname_elytra` 的命名规则。

下面是一个配置示例：

```yaml
forest_elytra:
  itemname: "Forest Elytra"
  material: ELYTRA
  Pack:
    texture: nexo:item/nexo_armor/forest_elytra_icon
  Components:
    equippable:
      slot: CHEST
      model: nexo:forest_elytra
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Nexo 自带的森林鞘翅</p></figcaption></figure>
