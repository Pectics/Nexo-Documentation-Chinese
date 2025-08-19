---
description: How to add new glyphs to the game?
cover: https://i.imgur.com/T76ianD.png
coverY: 0
---

# 🌀 字形

## 什么是字形？

字形是一个带纹理的 Unicode 符号。它可以在游戏内任何渲染文字的地方使用（聊天、物品名称、描述等）。它们可以用来实现非常强大的功能（自定义背包、额外状态栏），但最简单的用途就是表情符号。

## 配置一个字形

你可以在 glyphs 目录下的任意 YAML 文件中添加自己的配置段。
一个字形有几个主要属性：`texture`、`ascent`、`height` 和 `font`
`texture` 是纹理文件的路径和名称，格式为 `namespace:path`
`height` 是字形的高度比例，同时高度不能小于 ascent。
`ascent` 是字形的垂直偏移，必须小于或等于高度。
`font` 是你想要使用的字体。如果未指定，将会使用 settings.yml 中 `Glyphs.default_font` 的默认字体。
除非你需要在游戏的 ESC 菜单中使用字形，因为此处只支持 `minecraft:default` 字体，所以为了避免冲突和意外使用，你需要指定自定义字体。

你也可以为字形设置一个 `permission` 来限制谁能使用它。
如果未指定，Nexo 会使用 settings.yml 中定义的默认权限 `Glyphs.default_permission`。你可以指定 `<glyph_id>` 或 `<glyph_placeholder>`，Nexo 会自动替换。

字形还可以定义 `placeholders`，让玩家在聊天中更方便地使用快捷符号。
这是一个字符串列表，可以让玩家通过简写来调用某个字形。

```yaml
heart:
  texture: default/chat/heart
  ascent: 8
  height: 8
  #font: namespace:fontname     可选，未指定则使用 settings.yml 中的字体
  #permission: nexo.glyph.heart 可选，未指定则使用 settings.yml 中的权限
  #placeholders:
  #  - "<3"
```

{% hint style="warning" %}
如果你的纹理超过 256x256 分辨率，你需要缩小它，或者制作一个 [multi-bitmap-glyph.md](multi-bitmap-glyph.md "mention")
{% endhint %}

### 如何使用字形

Nexo 为每个字形实现了一个自定义 MiniMessage 标签，你几乎可以在任意位置使用它。
你可以使用 `<glyph:glyphid>` 来显示字形，把 glyphid 替换成你的字形 ID。上面的例子中就是 `heart`。
这个标签可以在 Tab 列表、计分板、标题、聊天前缀（如 LuckPerms）中使用。
建议尽量使用 Glyph 标签而不是原始 Unicode。

字形标签还可以传递一些可选参数。
对于 [multi-bitmap-glyph.md](multi-bitmap-glyph.md "mention")，你可以指定显示的索引。
例如如果你制作了一个 2x2 的字形，可以使用 `<glyph:heart:2>` 或 `<glyph:heart:2..3>` 来只显示字形的部分内容。

如果你希望字形可变色，可以使用 `<glyph:heart:colorable>` 或 `<glyph:heart:c>`&#x20;
这样字形就会继承前面应用的颜色，而不会强制显示为白色或默认颜色。

从 1.21.4 开始，还新增了 "shadow-color" 标签，允许修改字形阴影的颜色和透明度。
你可以通过 `shadow` 或 `s` 参数来使用，例如：`<glyph:heart:shadow:#AARRGGBB>`

所有这些参数都可以组合使用，你可以同时指定位图索引、设置可变色、修改阴影。

### 自定义 GUI

通过 Nexo 字形你可以创建自定义纹理 GUI。
Nexo 并不处理 GUI 背包的逻辑部分，只负责视觉部分。
只需像下面这样配置一个字形：

```yaml
customshop:
  texture: required/ui/menu_items
  #font: minecraft:my_font      # 可选，默认为 minecraft:default
  ascent: 37
  height: 256
```

然后在背包标题中输入 `<glyph:glyphid>`，Nexo 会处理剩下的部分。
这适用于绝大多数使用字形的场景。如果标签不起作用，你可以使用 [PlaceholderAPI 占位符](./#placeholderapi)。

要调整字形在背包中的水平位置，可以使用 shift 标签。
例如：`<shift:-8>` 会向后移动 8 像素，`<shift:211>` 会向前移动 211 像素。

### 表情符号列表

要让某个字形出现在 `/nexo emojis` 下，你需要明确指定它是一个 emoji：

```yaml
heart:
  texture: default/chat/heart
  is_emoji: true
```

默认情况下，只有玩家拥有权限时才会显示对应的表情。
在 `settings.yml` 中你可以切换 `only_show_emojis_with_permission` 选项。
启用后将会向所有玩家显示所有表情，并在悬停时提示他们是否有权限。![img](https://cdn.discordapp.com/attachments/758785982005903431/1002564595099111474/unknown.png)

占位符可由拥有权限的玩家在聊天中使用（如果指定了权限，非必须）。

## 如何让字形支持 Tab 补全？

只需在聊天配置中设置 `tabcomplete: true`。如果未指定，默认值为 `false`。

默认情况下，Tab 补全会使用原始 Unicode。这仅适用于使用默认字体（未指定字体时使用）的字形。
如果你希望它使用聊天占位符，可以在 settings.yml 中禁用 `unicode_completions`。

```yaml
myemoji:
  #font: minecraft:default
  tabcomplete: true
  placeholders:
    - "<3"
  permission: "nexo.emoji.heart"
```

## PlaceholderAPI

### 我的字形占位符是什么？

配置段名称就是字形 ID。在这个例子中，字形 ID 是 `heart`，对应的占位符是 `%nexo_glyphid%`，也就是 `%nexo_heart%`。
Glyph-ID 是任意字形配置的第一行，不是纹理名或占位符。你还可以在 PAPI 中使用 shift，例如 `%nexo_shift_-8%` 或 `%nexo_shift_8%`。

注意，如果字形的字体不是 `minecraft:default`，它将会默认使用字形标签，而不是 Unicode。
