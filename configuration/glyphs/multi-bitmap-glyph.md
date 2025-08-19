# 🖼️ 多位图字形

如果你有一个包含多个表情的纹理，或者一个超过 256x256 限制的纹理，你可以将它设置为多位图。
这意味着你可以将多个 Unicode 绑定到一张图片上。
在字形配置中，你可以指定所需的行数和列数。
这样 Nexo 会根据你的需要来分配 Unicode。

使用 512x512 纹理的示例：

{% code lineNumbers="true" fullWidth="false" %}
```yaml
myglyph:
  #texture: required/ui/menu_items
  #ascent: 37
  #height: 256
  rows: 2     # 告诉 Nexo 在分配 Unicode/字符时，该字形需要 2 行
  columns: 2  # 告诉 Nexo 在分配 Unicode/字符时，该字形需要 2 列
```
{% endcode %}

这将让 Nexo 为该字形分配 4 个 Unicode，并在使用时显示出来。

需要注意的是，在某些情况下不支持换行。例如在物品描述 (lore) 中，它无法正确对齐字形。解决方法是使用字形标签中的“范围索引”。以下是在 NexoItem 的 lore 中的示例：

```yaml
myitem:
  lore:
    - "<glyph:myglyph:1..2>"
    - "<glyph:myglyph:3..4>"
```

这样可以在 lore 中正确对齐字形。而在支持换行的场景中，你无需指定这样的范围，Nexo 默认会将其附加到文本中并正确对齐。
