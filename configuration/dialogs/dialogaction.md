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

# DialogAction

DialogAction 分为两类：**静态 (Static) 与 动态 (Dynamic)**。
静态动作不依赖输入字段的值。
动态动作可以结合输入字段的值来使用。

### 静态动作

静态动作的类型包括 [OPEN\_URL](https://minecraft.wiki/w/Dialog#open_url)、[RUN\_COMMAND](https://minecraft.wiki/w/Dialog#run_command)、[SUGGEST\_COMMAND](https://minecraft.wiki/w/Dialog#suggest_command)、[CHANGE\_PAGE](https://minecraft.wiki/w/Dialog#change_page)、[CLIPBOARD](https://minecraft.wiki/w/Dialog#copy_to_clipboard)、[SHOW\_DIALOG](https://minecraft.wiki/w/Dialog#show_dialog) 和 [CUSTOM](https://minecraft.wiki/w/Dialog#custom)。

```yaml
action:
  type: RUN_COMMAND
  command: "nexo inventory"
```

### 动态动作

动态动作是指那些可以结合对话框中输入字段的值来使用的动作。
例如，可以运行一个命令，并将 DialogInput 文本字段中的文字作为参数。
动态动作的类型包括 [DYNAMIC\_RUN\_COMMAND](https://minecraft.wiki/w/Dialog#dynamic/run_command) 和 [DYNAMIC\_CUSTOM](https://minecraft.wiki/w/Dialog#dynamic/custom)。
