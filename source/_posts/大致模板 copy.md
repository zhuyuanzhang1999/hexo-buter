---
title: OneNote转换markdown
tags:
  - GitHub
  - OneNote
id: '460'
categories:
  - - GitHub
date: 2023-03-17 21:50:00
---

### ConvertOneNote2MarkDown
一种常用的方法是使用一个PowerShell脚本来批量转换OneNote中的所有笔记本为Markdown文件，然后将这些文件上传到GitHub上。具体步骤如下：

下载或克隆这个仓库：https://github.com/SjoerdV/ConvertOneNote2MarkDown
安装Pandoc软件：https://pandoc.org/installing.html
打开PowerShell终端，导航到包含脚本的文件夹，运行命令：‘.ConvertOneNote2MarkDown.ps1’
输入一个空文件夹的路径，用来存储转换后的Markdown文件结构。
等待脚本执行完成，你会看到所有加载在OneNote中的笔记本都被转换为Markdown文件，并按照原来的层级结构保存在指定的文件夹中。
将这个文件夹上传到GitHub上，或者将其中的Markdown文件复制到你想要放入笔记的网页所在的仓库中。
注意：这个方法可能会丢失一些格式或内容，比如表格、图片、链接等。你可能需要手动检查和修改一些转换后的Markdown文件，以保证它们能正确显示在GitHub上。