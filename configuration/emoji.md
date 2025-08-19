---
description: 如何在游戏中添加表情符号？
---

# 表情符号 (Emoji)

## 什么是字形 (Glyph)？

字形是带有纹理的 Unicode 符号。它可以用于任何文本（聊天、物品名称、描述等）。\
它们可以实现非常强大的功能（例如自定义界面、额外状态条），但最简单的用途就是作为表情符号。

## 如何添加一个字形？

首先你需要创建一个 PNG 贴图。例如 `default/chat` 文件夹中的 `heart.png`。

![heart.png](../.gitbook/assets/heart%20%281%29.png)

然后在 `font.yml` 中添加你的字形配置。每个字形必须使用不同的 `code`。\
`code` 对应要使用的 Unicode 字符编号。\
`texture` 是贴图文件的路径和名称。\
`height` 决定显示字符的缩放，`ascent` 决定显示结果的垂直偏移。

```yaml
heart:
  code: 3000
  texture: default/chat/heart
  ascent: 8
  height: 8
```

## 如何在聊天中使用？

你需要在字形配置中添加一个聊天子配置：

```yaml
chat:
  placeholders:
    - "<3"
  permission: "nexo.emoji.heart"
```

玩家可以在聊天中使用这些占位符，前提是他们拥有所需的权限（如果配置了权限，权限并不是必需的）。

## 如何在物品名称或描述中使用？

任何字形都可以在物品配置的名称或描述中使用：

```text
<glyph:heart>
```

其中 `heart` 替换为你的字形配置名称。
