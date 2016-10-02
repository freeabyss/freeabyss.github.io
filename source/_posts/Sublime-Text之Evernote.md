---
title: Sublime Text之Evernote
date: 2016-09-13 21:27:26
tags: [sublime, markdown]
categories: [sublime]
---

# Evernote

下载了`Evernote`之后可以用Markdown编写印象笔记了。 [sublime evernote主页](https://github.com/bordaigorl/sublime-evernote)

## 功能

|功能|说明|commond|
|:---|:--|:----|
|Delete Node|删除笔记||
|Search Note|搜索笔记||
|Show Attachments|显示当前笔记的附件||
|Attach current file to a note|将当前文件作为附件发送给指定笔记||
|Insert Attachment Here|在光标处插入附件||
|Delete Attachment|删除附件||
|View Note in Web App|打开该笔记的网页版||
|View Note in Evernote client|在客户端中打开该笔记||
|Update Evernote Note|更新笔记|save_evernote_note|
|Send to Evernote as new note|创建新笔记send_to_evernote|
|Create New Notebook|创建新的笔记本||
|Open Evernote Note| 打开笔记|open_evernote_note|
|Clip to Evernote as new note|将当前选中的内容作为新的笔记创建||
|List linked notes|显示当前笔记引用的其它笔记链接||
|Insert link to a note|插入其它笔记的链接||

## 配置

访问[Developer Tokens](https://app.yinxiang.com/api/DeveloperToken.action)获取Token，打开Evernote.sublime-settings

```shell
{
    "noteStoreUrl": "https://app.yinxiang.com/shard/s1/notestore",
    "token": ""
}
```

### 添加快捷键示例

```shell
{ "keys": ["super+e"], "command": "show_overlay", "args": {"overlay": "command_palette", "text": "Evernote: "} },
{ "keys": ["ctrl+e", "ctrl+s"], "command": "send_to_evernote" },
{ "keys": ["ctrl+e", "ctrl+o"], "command": "open_evernote_note" },
{ "keys": ["ctrl+e", "ctrl+u"], "command": "save_evernote_note" },
```

### 个性化配置

  * md_syntax：定义md语法
  * inline_css：定义部分CSS样式
  * code_highlighting_style：代码高亮样式，autumn, default, github, monokai, perldoc, vim, borland, emacs, igor, murphy, rrt, vs, bw, friendly, native, tango, xcode, colorful, fruity, manni, pastie, trac