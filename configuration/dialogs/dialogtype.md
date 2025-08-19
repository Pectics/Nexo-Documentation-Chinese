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

# DialogType

对话框 (Dialog) 的核心在于选择你想要使用的类型。
可选项包括 [CONFIRM](https://minecraft.wiki/w/Dialog#confirmation)、[LIST](https://minecraft.wiki/w/Dialog#dialog_list)、[MULTI](https://minecraft.wiki/w/Dialog#multi_action)、[NOTICE](https://minecraft.wiki/w/Dialog#notice) 与 [LINK](https://minecraft.wiki/w/Dialog#server_links)。
默认类型是 NOTICE。

#### DialogAction

大多数类型都包含一个或多个 **DialogAction**，其格式如下所示：

```yaml
action:
  label: "<red>Action Label"
  tooltip: "<red>Action Tooltip"
  width: 150
```

#### Notice 类型

```yaml
type: NOTICE
action:
  ...
```

#### 确认类型 (Confirmation Type)

包含两个属性：**yes** 和 **no**，它们都是 **DialogActions**

```yaml
type: CONFIRM
yes:
  ...
no:
  ...
```

#### 列表类型 (Dialog List Type)

包含一个 **DialogAction** 属性 `exitAction`。
此外还包含 `buttonWidth`、`columns` 与 `dialogs` 属性。

**buttonWidth -** 按钮的宽度，范围 1 -> 1024，默认 150
**columns -** 列数，必须大于等于 0，默认 2
**dialogs -** 要显示的对话框 ID 列表

```yaml
type: LIST
buttonWidth: 150
columns: 2
dialogs:
  - "my_dialog"
exitAction:
  ...
```

#### 多操作类型 (Multi Action Type)

**exitAction -** 一个 **DialogAction**
**actions -** 一个 **DialogActions** 列表
**columns -** 列数，必须大于等于 0，默认 2

```yaml
type: MULTI
columns: 2
exitAction:
  ...
actions: [ ... ]
```

#### 服务器链接类型 (Server Links Type)

**buttonWidth -** 按钮的宽度，范围 1 -> 1024，默认 150
**columns -** 列数，必须大于等于 0，默认 2
**exitAction -** 一个 **DialogAction**

```yaml
type: LINK
exitAction:
  ...
columns: 2
buttonWidth: 150
```
