# ☄️ Oraxen → Nexo

从 Oraxen 迁移到 Nexo 已实现完全自动化。
只需将 Nexo 插件 jar 放到 plugins 文件夹并启动服务器，
Nexo 就会自动复制 Oraxen 的所有资源包内容、物品和字形。
同时，它也会复制所有设置与机制，并做必要调整。

{% hint style="warning" %}
尽管迁移应当是无障碍的，但仍强烈建议在切换到 Nexo 前为你的世界文件夹做好备份。
迁移过程中可能会有小疏漏，导致部分家具或自定义方块的轻微丢失。
{% endhint %}

{% stepper %}
{% step %}
**将 Nexo JAR 放入 `ServerFolder/plugins`**
{% endstep %}

{% step %}

#### 复制 `plugins/Oraxen` -> `plugins/Nexo/converter/Oraxen`

`converter` 文件夹默认不存在，请手动新建。
Nexo 会从该文件夹中读取并转换内容，随后会删除它。
今后你获得的新资源包也可以放到这里，Nexo 会再次执行转换。
{% endstep %}

{% step %}
**确保移除 plugins 文件夹中的 Oraxen JAR**

同时建议进入 `Server/WORLD/datapacks` 删除 Oraxen 遗留的数据包。
{% endstep %}

{% step %}
**确保你已备份所有世界存档**

虽然迁移理论上应无碍，但仍强烈建议在切换到 Nexo 前备份世界文件夹。
迁移中可能会有小疏漏，造成部分家具或自定义方块的轻微丢失。
{% endstep %}

{% step %}
**启动服务器**
{% endstep %}
{% endstepper %}

### 资源包

Oraxen 与 Nexo 在资源包工作方式上有一些差异。
主要区别在于 Nexo 不再使用 `pack/models` 这类快捷目录。
这些快捷目录总是引发很多困惑，因此 Nexo 遵循正常结构：
`pack/models` -> `pack/assets/minecraft/models` 等。
此外，Nexo 支持更简单的外部资源包导入。
只需将任意资源包 `.zip` 文件或包含 `assets/...` 的资源包文件夹放入 `pack/external_packs`，它就会被包含进最终资源包中。

### 物品

当玩家加入时，Nexo 会自动将现有物品从 Oraxen 转换为 Nexo。
在检测到有变更的情况下，也会扫描并转换。
其中最显著的就是音符盒、绊线方块和家具机制的定义方式。

### 家具

放置过的 Oraxen 家具在加载时会自动转换为 Nexo 家具。
但基于物品展示框的家具可能会有问题，因为 Nexo 仅支持基于 ItemDisplay 的家具。
这些家具可以手动替换，或等待后续更新来处理。

主要的配置差异体现在座位、灯光与碰撞箱（屏障和交互）的定义方式上。
Nexo 支持多个交互碰撞箱、座位与灯光。
建议阅读 [家具机制](../mechanics/furniture-mechanic/) 以获取更多信息。

### 自定义方块

自定义方块同样会被转换。Oraxen 与 Nexo 在自定义变体计算上有差异。Nexo 在导入 OraxenItems 时会自动修正。
例如：`custom_variation: 1` -> `custom_variation: 51`
此外，部分机制的定义方式也有细微调整。
相关示例可以在 [音符盒机制](../mechanics/custom-block-mechanics/noteblock-mechanic/) 和 [绊线方块机制](../mechanics/custom-block-mechanics/stringblock-mechanic.md) 中找到。


**如果在转换过程中遇到任何问题，请告诉我！**
