# 🎞️ 动态字形

{% hint style="info" %}
这是 Nexo 1.8 的即将推出功能
{% endhint %}

通过 Nexo 你可以制作动态字形，或称为 GIF，它们可以用来为 GUI 或表情添加动画效果。
操作非常简单，Nexo 会自动完成将 GIF 文件转换为兼容格式的大部分工作。

只需将 GIF 文件放入资源包中。例如我们使用 `Nexo/pack/assets/nexo/textures/gifs/necoflap.gif`

### GIF-字形配置

```yaml
necoflap:
  gif: nexo:gifs/necoflap.gif
  ascent: 9
  height: 11
  #frame_count: X      可选，主要用于限制较大的 GIF
  #offset: X           主要用于当 GIF 帧没有完美对齐时
```

与普通字形不同，字体无法自定义，因为 Nexo 会自动为你设置。
纹理属性基于 `gif` 属性，你可以通过它来自定义。

{% hint style="warning" %}
GIF 依赖于核心着色器，并可能在版本更新时失效。
如果 GIF 的帧数过高，大型 GIF 也可能导致卡顿，请考虑优化你打算使用的 GIF。
{% endhint %}

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTAoAxayP9PrBtX9UQ5wa%2Fuploads%2FnciiMhz3TRl476nq82Kp%2F2025-05-26%2015-31-12.mp4?alt=media&token=c563fad9-3620-4285-b3f5-753a9b410d19" %}
聊天和文本展示中使用 GIF 的示例
{% endembed %}
