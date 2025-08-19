---
description: Nexo 1.4 中新增的特性
cover: ../../.gitbook/assets/huge_2025-04-23_14.33.14.png
coverY: 0
---

# 🛏️ 床机制

家具也可以作为床使用。床位可以像下面这样进行配置。
这既可以用来复刻原版床，也可以让家具用来躺下。
它的配置包含一个偏移量，以及是否跳过夜晚和重置幻翼的属性。
普通的床这两个属性都为 true，但如果你希望它是长椅之类的，就可以禁用这些功能。

```yaml
myitem:
  Mechanics:
    furniture:
      beds:
        - 0,0,0 true true # x,y,z 跳过夜晚 重置幻翼
```

<figure><img src="../../.gitbook/assets/huge_2025-04-23_14.33.14.png" alt=""><figcaption><p>Nexo 默认物品中包含的双人床</p></figcaption></figure>
