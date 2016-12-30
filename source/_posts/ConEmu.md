---
layout: git
title: Git Bash Here in ConEmu
date: 2016-12-29 10:18:09
tags:
---

# windows系统命令行工具ConEmu集成git环境
## 步骤
1. win+Alt+p 打开settings
2. 选中Integration选项，修改其中的三个选项：
```
Menu item:  ConEmu Here [Git Bash]
Command:    /single /cmd {Git Bash}
Icon file:  C:\Program Files (x86)\Git\mingw32\share\git\git-for-windows.ico
```
3.点击Register,再点击Save settings

## 注意事项
1. 低版本可能要修改 Startup > Tasks 选项中的{Git bash}为
```
"C:\Program Files\Git\bin\sh.exe" --login -i
```
2. git路径根据自己具体的路径而定，一般为: `C:\Program Files (x86)\Git`
3. 配置好后，点击右键可以看见 `ConEmu Here [Git Bash]` 选项，这个就是集成 git 环境的 ConEmu
