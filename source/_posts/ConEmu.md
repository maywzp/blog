---
layout: git
title: Git Bash Here in ConEmu
date: 2016-10-13 10:18:09
updated: 2016-10-13 10:18:09
tags: ['配置']
---

ConEmu 是一个带标签的 Windows 终端，提供多标签支持和丰富的自定义选项，是 Windows 下不可多得的 Console,可集成 git 环境。

# windows 系统命令行工具 ConEmu 集成 git 环境

## 步骤

1. win+Alt+p 打开 settings
2. 选中 Integration 选项，修改其中的三个选项：

```
Menu item:  ConEmu Here [Git Bash]
Command:    /single /cmd {Git Bash}
Icon file:  C:\Program Files (x86)\Git\mingw32\share\git\git-for-windows.ico
```

3.点击 Register,再点击 Save settings

## 注意事项

1. 低版本可能要修改 Startup > Tasks 选项中的{Git bash}为

```
"C:\Program Files\Git\bin\sh.exe" --login -i
```

2. git 路径根据自己具体的路径而定，一般为: `C:\Program Files (x86)\Git`
3. 配置好后，点击右键可以看见 `ConEmu Here [Git Bash]` 选项，这个就是集成 git 环境的 ConEmu
