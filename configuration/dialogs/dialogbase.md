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

# DialogBase

对话框 (Dialog) 有一个基础部分，其中包含了对话框的内容。
下面是你可以使用的属性

**title -** 对话框的标题，总是显示在屏幕上
**externalTitle -** 用于链接到该对话框的按钮名称，默认值为 title
**canCloseWithEscape -** 是否可以通过 Escape 键关闭对话框
**afterAction -** 在点击或提交动作后对对话框执行的操作。&#x20;
\* **NONE -** 保持当前对话框界面打开
\* **CLOSE (默认) -** 关闭并返回到之前的非对话框界面（如果有）
\* **WAIT\_FOR\_RESPONSE -** 将当前界面替换为“等待响应”界面
**bodies -** 添加到对话框界面的 DialogBodies 列表
**inputs -** 添加到对话框界面的 DialogInputs 列表

### [DialogBody](https://minecraft.wiki/w/Dialog#Body_format)

DialogBody 用于描述显示在标题与输入区域之间的内容。
它们相对简单，分为两类：MESSAGE 与 ITEM

**Message 类型** 需要一个宽度属性和一条消息字符串
该消息支持 MiniMessage 与 Nexo Glyphs 及 Shift 标签

**Item 类型** 有更多属性：
**description -** 使用 MiniMessage 字符串，可选宽度（默认 200）
**showDecorations -** 若为 true，会显示物品的数量和耐久条
**showTooltip -** 若为 true，当鼠标悬停时显示物品提示
**width -** 元素的水平大小，范围 1 到 256，默认 16
**height -** 元素的垂直大小，范围 1 到 256，默认 16

要创建一个 DialogBody，可以按照以下示例，指定 Body 元素的 key/id 及其属性：

```yaml
base:
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
```

### [DialogInput](https://minecraft.wiki/w/Dialog#Input_control_format)

DialogInput 会渲染在 DialogBody 元素下方，并拥有多种方式来接收玩家输入的信息。

共有四种输入类型：[TEXT](https://minecraft.wiki/w/Dialog#text)、[BOOL](https://minecraft.wiki/w/Dialog#boolean)、[NUMBER](https://minecraft.wiki/w/Dialog#number_range) 与 [SINGLE](https://minecraft.wiki/w/Dialog#single_option)。

#### 文本输入 (Text-Input)

一个简单的文本输入框，具有以下属性：
**width -** 文本输入框的宽度，范围 1 到 1024，默认 200
**labelVisible -** 控制输入框标签是否可见
**maxLength -** 文本输入的最大长度
**initial -** 打开对话框时输入框的初始值
**multiLineOptions -** 可选，指定该字段是否为多行

```yaml
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
```

#### 布尔输入 (Boolean-Input)

一个复选框，会根据其状态返回一个字符串值

**onTrue -** 当选中时返回的字符串值，默认 "true"
**onFalse -** 当未选中时返回的字符串值，默认 "false"
**initial -** 复选框的初始状态

```yaml
inputs:
  bool_key:  
    type: BOOL
    label: "<red>Boolean Input Label"
    initial: true
    onTrue: "true"
    onFalse: "false"
```

#### 数值范围输入 (NumberRange-Input)

一个数字滑块，用于返回数值

**width -** 滑块的宽度，范围 1 到 1024，默认 200
**labelFormat -** 用于构建标签的翻译键
**start -** 滑块的最小值
**end -** 滑块的最大值
**step -** 每个刻度的增量值，如果未指定，滑块没有刻度
**initial -** 打开对话框时滑块的初始值（介于 start 与 end 之间）

```yaml
inputs:
  number_key:
    type: NUMBER
    width: 200
    label: "<red>Number Input Label"
    labelFormat: "options.generic_value"
    start: 0
    end: 1
    initial: 0.5
    step: 0.1
```

#### 单选输入 (SingleOption-Input)

**labelVisible -** 是否在按钮上显示标签
**width -** 按钮的宽度
**options -** 按钮可用的选项列表，包含一个 **display** 文本字段与一个 **initial** 字段

```yaml
inputs:
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
