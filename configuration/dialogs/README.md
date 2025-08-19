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

# 🗨️ 对话框 (Dialogs)

Nexo 简化了在服务器中添加新对话框的过程。
不需要额外制作数据包，你只需在 `plugins/Nexo/dialogs` 文件夹中编写一个 YAML 文件即可。

对话框由几个部分组成：
一个 [DialogType](dialogtype.md) —— 定义对话框的根属性
一个 [DialogBase](dialogbase.md) —— 定义对话框的内容

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>使用所有可用方法的对话框示例</p></figcaption></figure>

```yaml
type: NOTICE
action:
  label: "<red>Notice Label"
  tooltip: "<red>Notice Tooltip"
  width: 150
  action:
    type: RUN_COMMAND
    command: "nexo inventory"
base:
  title: "<red>Title"
  externalTitle: "External Title"
  canCloseWithEscape: true
  afterAction: CLOSE
  bodies:
    message_body:
      type: MESSAGE
      message: "<red>Some Message allowing MiniMessage"
      width: 200
    item_body:
      type: ITEM
      description: "Some Description"
     #description:
     #  contents: "<red>Some description"
     #  width: 200
      showDecorations: true
      showTooltip: true
      width: 16
      height: 16
  inputs:
    text_key:
      type: TEXT
      width: 200
      label: "<red>Text Input Label"
      labelVisible: true
      maxLength: 32
      initial: "Initial Input Text"
      multilineOptions:
        maxLines: 1
        height: 32
    bool_key:  
      type: BOOL
      label: "<red>Boolean Input Label"
      initial: true
      onTrue: "some_action"
      onFalse: "some_action"
    number_key:
      type: NUMBER
      width: 200
      label: "<red>Number Input Label"
      labelFormat: "options.generic_value"
      start: 0
      end: 1
      initial: 0.5
      step: 0.1
    single_key:
      type: SINGLE
      width: 200
      label: "<red>Single Input Label"
      labelVisible: true
      options:
        option_1:
          display: "First Option"
          initial: true
        option_2:
          display: "Second Option"
          initial: false
```

