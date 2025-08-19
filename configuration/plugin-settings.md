---
description: 各种影响插件整体运行的选项
hidden: true
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825582216237126/unknown.png
coverY: 0
---

# ⚙️ 插件设置

## 物品配置

### Nexo 配置概览？

Nexo 的配置主要分为三类：items、resourcepack 和 glyphs。
这些文件夹包含了大部分你需要的自定义配置。

## 资源包

### 混淆

混淆通过将所有模型、纹理和文件重命名为随机的命名空间和路径来实现。
这样可以让别人很难直接下载并在你的服务器外使用你的资源包。
它有三种模式：SIMPLE、FULL 和 NONE

此外还有一个选项可以缓存混淆后的资源包。
这意味着除非有更改，Nexo 不会重新混淆资源包。
这样玩家在每次服务器启动时就不必重新下载资源包。\\

```yaml
Pack:
  obfuscation:
    type: FULL
    cache: true
```

**NONE** 不会对资源包进行混淆

```makefile
📁ResourcePack
└── 📁assets
    └── 📁custom_namespace
        └── 📁models
             └── 📑custom_model.json
```

**SIMPLE** 仅混淆单个文件名，但保留原始的包结构

```makefile
📁ResourcePack
└── 📁assets
    └── 📁custom_namespace
        └── 📑02a61ae4-2457-4dfa-91af-9598cd52fd9e.json
```

**FULL** 会混淆整个路径

```
📁ResourcePack
└── 📁assets
    └── 📁0d003f53-e176-4e74-a895-d392c82f50be
        └── 📁models
             └── 📑02a61ae4-2457-4dfa-91af-9598cd52fd9e.json
```

### PackServer

Nexo 生成的资源包在发送给玩家之前需要托管在某个地方。
Nexo 内置了两种服务器选项：POLYMATH 和 SELFHOST

**POLYMATH** 是 Nexo 自带的远程服务器
它位于德国，因此可能会因为服务器位置和玩家下载速度而变慢

**SELFHOST** 是在本地机器上托管的服务器，如果你的玩家距离较近，速度可能会更快。你需要手动配置服务器的 IP 地址。

```yaml
Pack:
  server:
    type: SELFHOST
      selfhost:
        public_address: 0.0.0.0   # 设置为你的服务器 IP
        port: 8082                # 设置为你在服务器上已开放的端口
      polymath:
        server: atlas.mineinabyss.com
        secret: mineinabyss
```

### 分发

这一部分用于控制资源包何时发送给玩家。

```yaml
Pack:
  dispatch:
    # 在玩家进入服务器之前发送资源包
    # 大型资源包可能因为下载/加载时间过长而出问题
    send_pre_join: true
    send_on_join: false
    send_on_reload: true    # 使用 reload 指令后发送资源包给玩家
    delay: -1               # 延迟发送资源包，不适用于 PreJoin 分发
    mandatory: true         # 如果拒绝资源包则踢出玩家
    prompt: "<#fa4943>接受资源包以完整体验 <b><gradient:#9055FF:#13E2DA>Nexo</b><#fa4943> 的乐趣"
```

## 其他

### hide\_scoreboard\_numbers

此选项允许你隐藏计分板上的红色数字。

```yaml
  hide_scoreboard_numbers: true
```

### hide\_scoreboard\_background

此选项允许你隐藏计分板背景。

```yaml
  hide_scoreboard_background: true
```

### reset\_recipes

```yaml
reset_recipes: true
```

此选项可能会导致与其他配方插件冲突。如果你在重载 Nexo 时发现配方插件有 bug，可以禁用此选项。
如果你禁用了它，就需要重启服务器来刷新 Nexo 的配方。

## Nexo 背包界面

```yaml
nexo_inventory:
  main_menu_title: "<shift:-18><glyph:glyphid><shift:-193>"
  menu_rows: 6
  menu_layout:
    my_item:
      slot: 1
      icon: itemid
      title: <main_menu_title>ItemID
```

这允许你为 Nexo 背包界面的每个部分配置图标。
你可以使用 Nexo 的物品 id 或 Minecraft 的材料名。
