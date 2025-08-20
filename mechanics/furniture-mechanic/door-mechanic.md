---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# 🚪 门机制

Nexo 允许你创建一种作为门的家具。
你还可以指定一些额外的选项来实现更多行为：

**toggle\_hitbox\_on\_open** - 打开时将碰撞箱从屏障切换为交互实体
**open\_sound -** 打开门时播放的音效
**close\_sound -** 关闭门时播放的音效
**open\_properties -** 与 [家具属性](./#furniture-properties) 相同，但仅在开启状态下生效
**is\_sliding -** 指定门是滑动门还是普通门

新增了一个 **delay 属性**，用于定义门的“开启时间”。
如果未指定，门会立即改变状态。

门有两种类型：普通门和滑动门。滑动门通过应用 open\_properties 中的变换来实现开启，而普通门则是通过旋转实现。

**配置示例：**

{% columns fullWidth="true" %}
{% column width="50%" %}
{% code fullWidth="false" %}
```yaml
large_wooden_door:
  itemname: Large Wooden Door
  Pack:
    model: nexo:item/nexo_furniture/large_wooden_door
  Mechanics:
    furniture:
      limited_placing:
        floor: true
      hitbox:
        barriers: 0..1,0..2,0
      block_sounds:
        place_sound: block.wood.place
        break_sound: block.wood.break
      properties:
        translation: 0,1,0
        delay: 4
      door:
        open_sound: block.wooden_door.open
        close_sound: block.wooden_door.close
        toggle_hitbox_on_open: true
        open_properties:
          translation: -0.85,1,0
```
{% endcode %}
{% endcolumn %}

{% column width="50%" %}
{% code fullWidth="true" %}
```yaml
large_wooden_sliding_door:
  itemname: Large Wooden Sliding Door
  Pack:
    model: nexo:item/nexo_furniture/large_wooden_door
  Mechanics:
    furniture:
      limited_placing:
        floor: true
      hitbox:
        barriers: 0..1,0..2,0
      block_sounds:
        place_sound: block.wood.place
        break_sound: block.wood.break
      properties:
        translation: 0,1,0
        delay: 4
      door:
        is_sliding: true
        open_sound: block.wooden_door.open
        close_sound: block.wooden_door.close
        toggle_hitbox_on_open: true
        open_properties:
          translation: -1.5,1,0
```
{% endcode %}
{% endcolumn %}
{% endcolumns %}

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTAoAxayP9PrBtX9UQ5wa%2Fuploads%2Fs8AfcHvnoLucixCBnQlR%2F2025-08-19%2015-57-54.mp4?alt=media&token=cc47ff3d-876b-46a0-8c02-ec72d214423f" %}
