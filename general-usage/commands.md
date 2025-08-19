---
description: 插件指令的简单说明
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827022758330398/unknown.png
coverY: 0
---

# ⌨️ 指令

## 基本信息

所有 Nexo 指令都在 `/nexo` 下。

## 获取物品

### Nexo-Inventory 指令

这种方法的主要优点是它可以让你按 `Nexo/items/filename.yml` 分类同时查看所有物品。
你可以在这里获取物品的副本，但不能给予其他玩家。

#### 用法: `/nexo inventory` 或 `/nexo inv`

#### 权限: `nexo.command.inventory`

### Item-Give 指令

这个指令主要用于你想要给其他玩家物品，或者你想要实现自动发放物品的时候。

#### 用法: `/nexo give <item> [amount] [player]`

#### 权限: `nexo.command.give`

## 配方指令

这个指令允许你直接在游戏中使用配方生成器将新配方添加到配置中。更多使用方法请查看 [配方](recipes.md)。

#### 用法:

```yaml
/nexo recipe builder <builder> # 创建一个 <builder> 类型的配方生成器并打开它
/nexo recipe save <name> # 将你的配方保存为 <name>
/nexo recipe show all # 显示已加载的所有配方
/nexo recipe show <recipe> # 显示某一个配方
```

#### 权限: `nexo.command.recipes`

## Pack 指令

这个指令允许你将资源包发送给一组玩家。
当自动发送失败或者用于测试时很有用。

#### 用法: `/nexo pack <player>`

#### 权限: `nexo.command.pack`

## Item-Info 指令

这个指令允许你打印 NexoItem 的常规信息，用于调试。

#### 用法: `/nexo iteminfo <itemid>`

#### 权限: `nexo.command.iteminfo`

## Reload 指令

这个指令允许你重新加载 Nexo 的配置。
重新加载物品会更新你所做的更改，并更新玩家手中的所有旧副本。
重新加载资源包会重新生成资源包，如果在 `settings.yml` 中启用了 `Pack.dispatch.send_on_reload`，则会分发给所有玩家。

#### 用法

```yaml
/nexo reload # 重新加载物品配置，重新加载配方配置，重新生成资源包并上传
/nexo reload items # 重新加载物品配置
/nexo reload pack # 重新生成资源包并上传
/nexo reload recipes # 重新加载配方配置
```

#### 权限: `nexo.command.reload`

## Debug 指令

这个指令仅用于切换 Nexo 的调试状态。
当你遇到 bug 或错误时，可能会被要求开启它，以便提供更完整的错误日志。

#### 权限: `nexo.command.debug`
