---
description: 如何自定义物品外观？
---

# 物品外观

这个文件夹（`./plugins/Nexo/pack`）包含了你的资源包。它的工作方式和普通的 Minecraft 纹理包类似，但更简单。
你可以将纹理放入 `textures` 文件夹，将模型放入 `models` 文件夹。
你也可以在这些文件夹内创建子文件夹让结构更整洁，但这不是必须的。
当插件生成资源包时，它会在这个文件夹下生成名为 `pack.zip` 的文件。

### 创建一个简单的 2D 物品

将所需的纹理放在资源包文件夹的 `textures` 目录下。
然后你可以让 Nexo 通过叠加纹理来生成模型：

```yaml
  Pack:
    generate_model: true
    parent_model: "item/handheld"
    textures:
      - example_image1.png # png 后缀不是必须的
      - example_image2.png
```

`parent_model` 字段是 Minecraft 必需的。实际上它会让你的物品继承 Minecraft 模板物品的渲染属性。
你可以查看 Minecraft 的默认模型来寻找可用的模板，但我个人通常将 `item/handheld` 用于剑类等武器，而 `item/generated` 用于简单物品或宝石类（如紫水晶）。

你也可以使用另一种声明纹理的方式，这在使用方块父模型时尤其方便。

```yaml
Pack:
  generate_model: true
  parent_model: "block/cube"
  textures:
    top: example_image.png
    side: example_image2.png
```

### 使用 json 模型

创建一个 json 模型可能比较耗时，但它能让你制作非常酷的东西（比如 3D 物品）。
在 Nexo 中整合 json 模型非常简单。
将纹理放入 `textures` 文件夹，将模型放入 `models` 文件夹（位于 `Nexo/pack/assets/minecraft` 内）。
然后你就可以让 Nexo 将该模型应用到你的物品上：

{% hint style="danger" %}
模型和纹理的文件名必须全部小写。从 Minecraft 1.11 起，原版已不再支持大写（虽然使用 OptiFine 的玩家仍然可以加载）。
{% endhint %}

```yaml
  Pack:
    generate_model: false
    model: example_model.json # json 后缀不是必须的
```

#### ⚠️ 使用 json 模型时的专业提示！

通常你获得的模板会将纹理放在某个文件夹中。为了确认这一点，打开 json 文件并查看前几行，你会看到类似内容：

```json
{
	"textures": {
		"particle": "custom/bonesword_palette",
		"texture": "custom/bonesword_palette",
		"bonesword_palette": "custom/bonesword_palette"
	},
	...
```

可以看到，纹理路径是 **custom/bonesword\_palette**，这意味着 Minecraft 会在 `custom` 文件夹中查找名为 **bonesword\_palette.png** 的纹理文件。
所以你需要在 `Nexo/pack/assets/minecraft/textures` 内创建 `custom` 文件夹。
你也可以去掉 `custom/`，只保留纹理名，这样只需把文件直接放在 `textures` 文件夹中，而无需创建子文件夹。

### 使用带有格挡模型的 json（用于盾牌）

如果你想为盾牌使用自定义模型，你需要指定格挡时的模型，也就是玩家右键使用盾牌时的显示模型。
在 Nexo 中，这也很简单，配置示例如下：

```yaml
  Pack:
    generate_model: false
    model: example_shield.json # json 后缀不是必须的
    blocking_model: example_shield_blocking.json # json 后缀不是必须的
```

