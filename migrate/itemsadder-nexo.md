# 📦 ItemsAdder → Nexo

相比从 Oraxen 迁移，ItemsAdder 需要更多的手动步骤。
Nexo 会尽可能自动化处理，但由于 ItemsAdder 的一些奇怪设计，有些内容无法直接迁移。
Nexo 会尽可能转换所有物品、字形/字体图像和资源包。

{% hint style="warning" %}
这不太可能是一个完美无缺的过程，因此请务必先做好备份，并在测试服务器上尝试。
{% endhint %}

{% hint style="danger" %}
此转换器适用于 ItemsAdder v4
ItemsAdder v3.x 尚未经过测试，可能会出现转换问题。
建议在转换到 Nexo 之前，先使用 ItemsAdder 的内部更新流程。
{% endhint %}

{% stepper %}
{% step %}
**将 Nexo JAR 放入 `Server/plugins` 文件夹中**
{% endstep %}

{% step %}

#### 复制 `plugins/ItemsAdder` -> `plugins/Nexo/converter/ItemsAdder`

`converter` 文件夹默认不存在，请手动新建该文件夹。
Nexo 会从此文件夹中读取并转换内容，随后会删除该文件夹。
今后你获得的新资源包也可以放到这里，Nexo 会再次执行转换。
{% endstep %}

{% step %}
**备份你的所有世界存档**

尽管迁移理论上应该无碍，但仍强烈建议在切换到 Nexo 前，先为世界文件夹做备份。
迁移过程中可能会有小疏漏，导致部分家具或自定义方块的轻微丢失。
{% endstep %}

{% step %}
**移除 ItemsAdder 和 LoneLibs 的 JAR 文件**

保留 `plugins/ItemsAdder` 文件夹，因为 Nexo 会从这里读取并转换内容。
同时保留它也有利于在未来需要再次迁移时作为备份。
{% endstep %}

{% step %}
**启动你的服务器**
{% endstep %}

{% step %}
**检查控制台中的转换问题，并测试物品/字形**
{% endstep %}
{% endstepper %}

<mark style="color:red;">资源包</mark> 内容会被打包到 `Nexo/pack/external_packs/ItemsAdder/namespace/...` <mark style="color:green;">物品</mark> 会被移动到 `Nexo/items/itemsadder/...` <mark style="color:yellow;">字形/字体图像</mark> 会被移动到 `Nexo/glyphs/itemsadder/namespace/...`

### <mark style="color:yellow;">已知问题</mark>

Nexo 无法实现 100% 的迁移，因为有些功能在不同插件间根本不可行。
最常见的问题是：在世界中已放置的家具如果不是基于 Display Entities，则无法被自动转换。
Nexo 会尽力将配置文件转换为自己的格式，这意味着新放置的家具应当能保持原有外观。
