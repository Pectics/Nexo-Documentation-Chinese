---
icon: file-zipper
---

# 📂 资源包

### 资源包结构

Nexo 中的资源包遵循原版结构，但同时允许你导入并自动合并完整的资源包。
这样做是为了让导入第三方资源包更加方便。
下面是新结构的示例。

{% code title="" %}
```
📁Nexo
└── 📁pack
    └── 📁assets
    │    ├── 📁minecraft
    │    │    ├── 📁models
    │    │    │    ├── 📁item
    │    │    │    │    └── 📑paper.json
    │    │    │    └── 📑custom_model.json
    │    │    └── 📁textures
    │    │         └── 🖼️something.png
    │    └── 📁custom_namespace
    │        └── 📁models
    │            └── 📑custom.json
    │  
    └── 📁external_packs
        ├── 📁DefaultPack.zip
        ├── 📁custom_resourcepack.zip
        └── 📁custom_resourcepack2
            └── 📁assets
                └── 📁custom_namespace2
```
{% endcode %}

目标是允许用户通过 ZIP 或目录的方式合并资源包，而不局限于普通的 assets 文件夹。
这会动态合并任何冲突的文件，例如 paper.json 或 sounds.json，而不是迁移到 oraxen 配置里重新生成。
这意味着你的资源包导入说明现在可以简化为：
把 `my_pack.zip` 放到 `Nexo/pack/external_packs` 文件夹里即可。

### 混淆

Nexo 内置了一种“混淆”资源包内容的方法。
它会随机化所有文件名，以尽可能让盗版者难以直接窃取内容。
它有三种模式：`NONE`、`SIMPLE`、`FULL`

**NONE** - 顾名思义，不做任何混淆
**SIMPLE** - 仅混淆文件名
`namespace:model/path.json` -> `namespace:bba2d60b-8e3e-4051-9734-fef92766777f`
**FULL** - 混淆命名空间和文件名;
`namespace:model/path.json` -> `c491303e-ba1e-4037-a59d-62b5fdfb6bb8:bba2d60b-8e3e-4051-9734-fef92766777f`

### PackSquash 集成

Nexo 允许你在不需要手动重新上传的情况下对资源包运行 PackSquash。
只需下载最新的 [PackSquash](https://github.com/ComunidadAylas/PackSquash/releases) 构建版本并将其放入 `plugins/Nexo/pack/packsquash`。
然后将 **packsquash.toml** 放在同一目录下，可以在 [这里](https://gist.github.com/Boy0000/92149d2704b6086473fccb4d771c42b4) 找到示例。
如果你希望它在另一个位置，可以为二进制文件和配置文件指定路径。

```yaml
Pack:
 generation:
    packsquash:
      enabled: true
      executable_path: plugins/Nexo/pack/packsquash/packsquash
      settings_path: plugins/Nexo/pack/packsquash/packsquash.toml
```

要启用 Nexo 的 PackSquash 集成，只需在 settings.yml 中启用 `Pack.generation.packsquash.enabled`。
然后当资源包生成时，它会启动 PackSquash 进程。
如果成功，你应该会看到如下的结果。

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>PackSquash 成功运行的示例</p></figcaption></figure>

如果失败，你将会看到详细的信息，包括具体的文件和失败原因。
如果启用了 Nexo 的 debug 模式，它还会输出所有成功处理文件的信息。

{% hint style="info" %}
根据你的 TOML 配置、资源包的大小和复杂度，PackSquash 过程可能需要一些时间。Nexo 会缓存输出结果，因此如果资源包没有更改，PackSquash 过程就不需要再次运行。
{% endhint %}

### PackServer

Nexo 提供了 3 种方式来上传和分发它生成的资源包
**POLYMATH** - 由 Nexo 团队托管的专用服务器，你的服务器会将资源包上传到这里
该服务器目前位于德国
**SELFHOST** - 在你自己的机器上运行的本地服务器。需要你配置 `public_address` 并确保指定端口开放
**LOBFILE** - 由 [LobFile](https://lobfile.com/) 托管的服务器，需要在 settings.yml 中配置 `api_key`
API 同时也支持扩展 `NexoPackServer-Interface`，以便你可以实现自定义方案。

### 跨服/代理资源包

Nexo 默认不支持在 velocity/bungee 网络下处理资源包。
不过这并非必须，因为玩家在切换服务器时会保留资源包，除非新服务器发送了新的资源包。

假设你有服务器 A、B 和 C：

1. 将服务器 B 和 C 的 Pack.server 设置为 NONE。这样玩家进入服务器 A 时会加载资源包，当他们切换到服务器 B 或 C 时，不会卸载服务器 A 的资源包。缺点是如果玩家从 B 或 C 再次进入 A，他们会重新接收并加载资源包。
2. 在 Velocity/Bungee 服务器上使用类似 [OneTimePack](https://www.spigotmc.org/resources/onetimepack-avoid-double-sending-the-same-pack-bungeecord-velocity.106749/) 的插件。这类插件会检查资源包请求并进行对比，如果是相同的资源包就会跳过发送。
   如果采用这种方式，请确保要么为你的 Nexo 资源包禁用 [混淆](resourcepack.md#obfuscation)，要么启用缓存并手动将 `.deobfCacheResourcepack` 文件夹复制到所有服务器。

### 导入

Nexo 支持多种方式导入第三方资源包。
推荐的方式如上所述：将目录或 .zip 文件放入 `plugins/Nexo/pack/external_packs`。
此外，你还可以在 settings.yml 中使用 `Plugin.import.from_location` 来指定相对于插件目录的文件夹/zip 文件。
你还可以使用 `Plugin.import.from_url` 在 settings.yml 中指定任意 URL，Nexo 会从该地址下载目录或 zip 文件并导入。
