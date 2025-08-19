# 🔗 引用字形

引用字形用于当你想要“引用”多位图字形中的某一部分时。
例如，如果你有一个包含 10 个表情的多位图字形，你可以像下面这样引用其中的某一个：

```yaml
multi_bitmap:
  texture: spritesheet
  rows: 2
  columns 5

#index 是行号与列号
first_emoji:
  reference: multi_bitmap
  index: 1
...
tenth_emoji:
  reference: multi_bitmap
  index: 10
```
