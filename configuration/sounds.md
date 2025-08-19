# 🎵 音效

Nexo 允许你注册可在 `/playsound` 或其他插件中使用的自定义音效。
最基础的音效可以通过编辑 `plugins/Nexo/sounds.yml` 来进行如下配置：

```yaml
sounds:
  - id: block.custom.mysound   # id: 命名空间:id
    sound: nexo:mysound.ogg    # 引用 assets/nexo/sounds/mysound.ogg
    #sounds:                   # 可选，多个音效时会随机选择一个
    #  - mysound.ogg
    #  - mysound2.ogg
```

你也可以根据需要调整更多属性，但大多数情况下，上面的默认配置已经足够。
每个属性的详细说明可以在 [这里](https://minecraft.wiki/w/Sounds.json) 找到。

```yaml
#https://minecraft.wiki/w/Sounds.json
sounds:
  - id: nexo:music.something
    sound: nexo:music/something.ogg
    sounds:                                  # 如果有多个音效文件，可在这里列出
      - nexo:music/something.ogg
      - nexo:music/something2.ogg
    stream: true                             # 可选，默认为 false
    preload: true                            # 可选，默认为 false
    volume: 1f                               # 可选，默认为 1f
    pitch: 1f                                # 可选，默认为 1f
    weight: 1                                # 可选，默认为 1
    attenuation_distance: 13                 # 可选，默认为 16
    jukebox_playable:                        # 可选，用于注册自定义唱片音效
      comparator_output: 15                  # 可选，默认为 15，取值范围 1..15
      range: X                               # 可选，若省略则音效范围为动态
      length_in_seconds: 2.5
      description: Description
```

其中的 `jukebox_playable` 用于注册在自定义唱片中播放的音效。
Nexo 会自动生成所需的数据包，你随后可以在物品的 [JukeboxPlayable-Component](items-advanced.md#components) 中引用它。

#### 替换音效

如果你想替换 Minecraft 原有的音效，可以这样做：

```yaml
sounds:
  - id: block.glass.place # 移除原版音效
    sounds: []
    replace: true
  - id: block.glass.break # 用自定义音效替换原版音效
    sound: nexo:customglasssound
    replace: true
```
