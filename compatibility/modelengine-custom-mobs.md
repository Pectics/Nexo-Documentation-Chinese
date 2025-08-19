---
description: 如何合并资源包？
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966831836904980610/unknown.png
coverY: 0
---

# ModelEngine - 自定义生物

ModelEngine 会生成一个资源包，其中包含所有自定义实体的模型和纹理。\
Nexo 会自动导入 ModelEngine 的资源包，并将其合并到自身的资源包中。\
出于历史兼容性考虑，Nexo 默认会移除该资源包中的核心着色器，因为它们常常导致资源包出错。\
\
如果你希望 Nexo 在自动导入时保留着色器，可以关闭 `Pack.import.modelengine.exclude_shaders`。
