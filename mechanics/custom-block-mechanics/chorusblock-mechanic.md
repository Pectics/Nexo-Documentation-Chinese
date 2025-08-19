---
icon: window-frame
---

# 紫颂方块机制 (ChorusBlock Mechanic)

{% hint style="info" %}
CHORUSBLOCK 类型最多允许 **63** 种自定义方块。
每个方块对应一个 `custom_variation`
{% endhint %}

### 创建你的第一个方块

#### 父模型 (Parent-Model)

Nexo 物品的根配置与普通物品相同（例如你可以用钻石等任意材料），并设置一个 itemname 等。
建议不要直接使用方块作为 material，而是使用像 PAPER 这样的材料。
在 Pack 部分，你可以为方块指定自定义模型或纹理。
如果你只有纹理，可以指定一个 `parent_model`，Nexo 会自动为你生成所需文件。
一个标准的 1x1x1 方块通常使用 `"block/cube_all"`。

```yaml
my_block:
  itemname: "My block"
  material: PAPER
  Pack:
    parent_model: "block/cube_all"
    texture: my_block_texture.png
```

### 自定义方块机制配置

要使用此机制，你需要告诉 Nexo 使用哪个模型（如果使用自动生成的模型，只需写上物品的名称 ID）。
接着需要指定一个未被其他方块占用的 `custom_variation` 值。
合法的 `custom_variation` 范围是 1..63。

```yaml
my_block:
  Mechanics:
    custom_block:
      type: CHORUSBLOCK
      custom_variation: 2
      model: my_block
      drop:
        silktouch: false
        minimal_type: STONE
        loots:
          - nexo_item: my_block
            probability: 1.0
```
