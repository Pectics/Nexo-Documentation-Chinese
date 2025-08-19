---
description: 关于 Nexo 最常见问题的总结
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# ❓ 常见问题

## Nexo 会生成一个资源包，那我还能用自己的资源包吗？

你可以将任何资源包合并到 Nexo 生成的资源包中。\
只需把 `.zip` 文件或文件夹放到 `Nexo/pack/external_packs` 目录下，\
插件就会将它合并到最终的资源包里，并发送给所有玩家。\
详细说明请查看资源包页面。

### 音符盒和绊线钩无法正常工作？

Nexo 使用音符盒和绊线作为自定义方块，因此会禁用它们在原版中的所有行为。\
不过，noteblock-mechanic 提供了选项，可以在保留自定义方块的同时重新启用原版行为，你可以在 `Nexo/mechanics.yml` 中进行设置。\
如果你不在乎自定义方块，也可以直接在 `mechanics.yml` 中禁用 noteblock 和 stringblock 机制。

## 我的纹理在使用 OptiFine 时有效，但在原版中无效

这通常是因为这些纹理或模型使用了仅 OptiFine 支持的格式。\
自 Minecraft 1.11 起，资源包的格式要求变得非常严格。\
文件名必须全部小写，不能包含空格，并且纹理大小不能超过 256x256。
