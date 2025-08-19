---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# 🖼️ 自定义画作

{% hint style="info" %}
Nexo 仅会为 1.21.3+ 的服务器生成数据包。你仍然可以在 1.21.1 上使用自定义画作，但需要手动制作数据包。
{% endhint %}

从 1.21 开始，你可以通过数据包制作自定义画作。Nexo 会基于 `Nexo/paintings.yml` 文件自动生成所需的数据包，从而简化这一流程。

下面是添加自定义画作的示例：

```yaml
paintings:
  nexo:custom_painting:
    author: boy0000
    title: <red>Custom Painting
    asset_id: nexo:custom_painting  # PNG 的路径，命名空间:路径
    width: 1     # 画作的宽度，以占用的方块数计
    height: 1    # 画作的高度，以占用的方块数计
    random_place: true # 会从原版画作中随机替换
  nexo:animated_painting:
    author: boy0000
    title: <red>Animated Custom Painting
    asset_id: nexo:animated_painting
    width: 1
    height: 1
```

然后，你只需将画作的贴图放入 Nexo 的资源包中，位置由 `asset_id` 指定。
所有画作贴图的路径为：`assets/NAMESPACE/textures/painting/PATH`。
配置格式与其他部分相同，使用 `NAMESPACE:PATH`。

以上示例中，贴图需要放在 `assets/nexo/textures/painting/custom_painting.png`。

### 动态画作

你也可以通过 MCMETA 文件来制作动态画作。
其中 `width` 和 `height` 属性表示每一帧在 PNG 中的像素大小。
下面是一个基本示例，更详细的说明可参考 [Minecraft Wiki](https://minecraft.wiki/w/Resource_pack#Texture_animation)。

{% code title="animated_painting.png.mcmeta" %}
```json
{
  "animation": {
    "width": 256,
    "height": 256,
    "frametime": 1
    
  }
}
```
{% endcode %}

该文件的命名需与贴图相同，并加上 `.mcmeta` 后缀。
在上面的示例中，路径应为：`assets/nexo/textures/painting/animated_painting.png.mcmeta`。

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTAoAxayP9PrBtX9UQ5wa%2Fuploads%2FNQBDM0CDYHw3xLDuMFvA%2F2025-07-19%2021-41-23.mp4?alt=media&token=84affb23-a6a7-491e-8053-d3bc14efc2f5" %}
静态画作与基于 MCMeta 的动态画作
{% endembed %}

### NexoItem

当你的自定义画作被注册后，你可以创建一个自定义 NexoItem 来放置对应的画作。下面是一个基本示例：

```yaml
custom_painting:
  itemname: Custom Painting
  material: PAINTING
  Components:
    painting_variant: nexo:custom_painting
animated_painting:
  itemname: Animated Painting
  material: PAINTING
  Components:
    painting_variant: nexo:animated_painting
```
