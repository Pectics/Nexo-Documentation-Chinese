---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966831327984893992/unknown.png
coverY: 0
---

# 🧑‍🌾 农业机制

### 它是如何运作的？

Nexo 拥有一个植物生长系统，可以定义不同的生长阶段，以下是配置示例。

**delay** 生长所需的时间（以刻为单位）
**probability** 当经过 delay 后生长的概率
**light\_boost** 当附近有光照时，生长速度加快
**next\_stage** 指定下一个阶段，它必须是一个已经创建的 Nexo 物品。

```yaml
rose_plant:
  itemname: "<gradient:#46EEAA:#2CBFC7>Rose Plant"
  material: COOKED_BEEF
  Pack:
    model: custom/plants/rose_stage_1

rose_seed:
  itemname: "<gradient:#46EEAA:#2CBFC7>Rose Seed"
  material: PAPER
  Mechanics:
    furniture:
      item: rose_plant_stage1
      evolution:
        delay: 10000
        probability: 0.5
        light_boost: true
        next_stage: rose_plant_stage1
      drop:
        silktouch: true
  Pack:
    model: custom/plants/rose_stage_1
```

### 第一阶段

```yaml
rose_plant_stage1:
  material: PAPER
  Mechanics:
    furniture:
      evolution:
        delay: 10000
        probability: 0.5
        light_boost: true
        next_stage: rose_plant_stage2
      drop:
        silktouch: true
  Pack:
    model: custom/plants/rose_stage_1
```

### 第二阶段

```yaml
rose_plant_stage2:
  material: PAPER
  Mechanics:
    furniture:
      evolution:
        delay: 10000
        probability: 0.5
        light_boost: true
        next_stage: rose_plant_stage3
      drop:
        silktouch: true
  Pack:
    model: custom/plants/rose_stage_2
```

### 第三阶段

```yaml
rose_plant_stage3:
  material: PAPER
  Mechanics:
    furniture:
      evolution:
        delay: 100000
        probability: 0.25
        light_boost: true
      drop:
        silktouch: true
        loots:
          - { nexo_item: rose_seed, max_amount: 2, probability: 0.75 }
          - { nexo_item: rose_plant, max_amount: 5, probability: 0.55 }
  Pack:
    model: custom/plants/rose_stage_3
```

植物可以拥有任意数量的阶段，但这些阶段必须是你自己创建的模型，而不是插件自动生成的模型，否则无法生效。
最后补充说明一个机制：**farmland\_required** —— 它要求植物只能种植在肥沃土壤上。

***
