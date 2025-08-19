# 🔳 交互碰撞箱

**交互实体碰撞箱** 需要设置 **偏移量 (offset)、宽度 (width) 和高度 (height)**，并且它们没有碰撞效果。
你可以在游戏中按下 F3+B 开启碰撞箱显示来查看这些碰撞箱。

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        interactions:
        # - 偏移量 宽度,高度
          - 0,0,0 1,1
          - 1,0,0 1,2.0
          - -1,0,0 1,2.2
```
