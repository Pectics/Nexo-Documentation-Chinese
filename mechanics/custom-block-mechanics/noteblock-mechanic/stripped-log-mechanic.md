---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827878706708560/unknown.png
coverY: 0
---

# 去皮木头机制 (Stripped Log Mechanic)

## 这是什么？

该机制允许你像原版一样，将自定义原木剥皮变成去皮版本。

### 配置示例

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      log_strip:
        stripped_log: stripped_log # 剥皮后变成的方块
        drop: bark # 右键剥皮操作后的额外掉落物
```

{% embed url="https://youtu.be/ohiGtlz_who" %}
