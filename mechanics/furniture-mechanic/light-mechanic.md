# 💡 灯光机制

通过灯光机制，你可以配置家具发光。
它需要一个相对于基础家具的 **offset（偏移量）**，以及一个介于 1 到 15 之间的 **light-level（光照等级）**。
灯光也可以设置为可切换，只需添加 `toggleable: true`，这样右键点击家具即可切换灯光开关。
使用 `toggled_model` 时，你可以提供一个 NexoItem 来显示灯光开启时的模型。
同样地，`toggled_item_model` 允许你直接提供一个 ItemModel（无需 NexoItem）来显示灯光开启时的效果。注意：此功能仅适用于 1.21.2+ 服务器。

```yaml
myitem:
  Mechanics:
    furniture:
      lights:
        #toggleable: false                    # 默认值为 false
        #toggled_model: some_nexo_item        # 灯光开启时显示的 NexoItem
        #toggled_item_model: namespace:model  # 灯光开启时使用的 ItemModel，仅适用于 1.21.2+
        lights:
          - 0,0,0 15    # x,y,z 光照等级
```

<div><figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Nexo 默认物品中的台灯（关闭状态）</p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Nexo 默认物品中的台灯（开启状态）</p></figcaption></figure></div>
