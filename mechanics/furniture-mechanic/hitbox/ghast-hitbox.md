# 👻 恶魂碰撞箱

**恶魂实体碰撞箱** 是 1.21.6+ 版本的新特性，允许使用可缩放的实体碰撞箱。
它需要设置 **偏移量 (offset)、缩放比例 (scale) 和旋转角度 (rotation)** 属性，并可选地添加 `visible` (true/false) 用于调试显示。
缩放比例默认是 0.25（即一个方块大小的碰撞箱），除非另行指定。
旋转角度默认是 0，除非另行指定。

{% hint style="warning" %}
此功能仅在 1.21.6+ 服务器上可用
{% endhint %}

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        ghasts:
        # - 偏移量 缩放比例 旋转角度 是否可见
          - 0,0,0 0.25
          - 0,1,0 0.25 45
          - 0,2,0 0.25 true
```
