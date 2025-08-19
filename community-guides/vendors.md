---
description: 面向供应商及其他希望为 Nexo 制作第三方资源包的指南
---

# 商人指南

下面是推荐的以“拖放”方式向 Nexo 添加内容的方法。\
以下示例将以一个名为 "NexoMC" 的商店为例。

### 资源包

在包含资源包时，理想方式是使用“外部资源包”。\
Nexo 支持合并多个完整的资源包，为了避免冲突，这是最佳做法。\
同时，最好使用合适的命名空间，而不是把所有内容都塞进默认的 `minecraft` 命名空间。\
例如：`Nexo/pack/external_packs/NexoMC/assets/nexomc/models/item/some_model.json`\
这样可以最大限度减少与其他资源包及物品可能产生的冲突。

```
📁Nexo
└── 📁pack
└── 📁external\_packs
├── 📁RequiredPack.zip         # Nexo 默认
├── 📁DefaultPack.zip          # Nexo 默认
└── 📁NexoMC
└── 📁assets
└── 📁nexomc
├── 📁models
\|   └── ...
└── 📁textures
└── ...
```

### 物品

Nexo 还改进了物品的组织方式，允许在 `Nexo/items` 中使用子文件夹。\
因此，推荐的预制物品配置文件存放方式为：`Nexo/items/NexoMC/nexo_christmas_furniture.yml`

```
📁Nexo
└── 📁items
└── 📁NexoMC
├── 📄 christmas\_furniture.yml
└── 📄 easter\_armor.yml
```

此外，与 Oraxen 相比，配置也有一些变化，主要涉及 [家具](../mechanics/furniture-mechanic/) 和 [自定义方块](../mechanics/custom-block-mechanics/) 机制：  
🟨 `itemid.Mechanics.furniture.display_entity_properties` → `itemid.Mechanics.furniture.properties`  
🟨 `itemid.displayname` → `itemid.itemname`  
🟨 `itemid.customname` 用于沿用 1.20.4 及以下的旧 “DisplayName” 逻辑  
🟨 家具碰撞箱结构已改变，详见 [文档](../mechanics/furniture-mechanic/#hitboxes)  
🟨 自定义方块机制已改变，详见 [音符盒](../mechanics/custom-block-mechanics/noteblock-mechanic/) / [绊线方块](../mechanics/custom-block-mechanics/stringblock-mechanic.md)  
❌ `itemid.Mechanics.furniture.type` —— Nexo 仅支持 Display-Entities  
❌ `itemid.Pack.generate_model` —— 模型生成由系统自动决定  
✔️ `itemid.Components.item_model` —— 在 1.21.2+ 可用，以避免完整的 `itemid.Pack` 配置  
✔️ `itemid.Pack.texture` —— 可用于只有单一纹理的情况  
✔️ `itemid.Pack.textures` —— 接受单个纹理、纹理列表或键值对映射  

### 字形

字形机制没有大的改动，但现在支持多个命名空间。\
与资源包相同，推荐使用单独的命名空间。

```yaml
santa_claus:
  texture: nexomc:santa_claus
  font: nexomc:christmas_glyphs
  ...
```

