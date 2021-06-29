---
title: 使用AutoHotKey映射常用快捷键
date: 2021-05-31 20:36:57
categories:
- [效率, windows]
tags:
- windows
---

## 前言
之前一段时间一直使用一台macbook pro，感觉苹果对系统的设计有很多值得称赞的地方。比如说系统快捷键，常用的快捷键比在windows下的更符合人的操作习惯。现在由于同时用win和mac两个平台，所以希望能有办法统一两个平台的快捷键。
## 方案
通过搜寻资料，常用的方案是AutoHotKey，还有较新的由微软官方推出PowerToys。

- AutoHotKey
> AutoHotkey 是一个自由、开源的宏生成器和自动化软件工具，它让用户能够自动执行重复性任务。AutoHotkey 可以修改任何应用程序的用户界面（例如，把默认的 Windows 按键控制命令替换为 Emacs 风格）。它是由定制的脚本语言驱动，旨在提供键盘快捷键或热键。——wikipedia

AutoHotKey实际上是一门脚本语言，功能强大，远不止映射快捷键。其可以通过编程的形式实现各种功能操作。但是需要学习语法，学习成本略高。

- PowerToys
> Microsoft PowerToys是一组免费的系统工具软件，由微软为Windows操作系统上的系统管理员设计。这些程序为系统加入或变更了一些功能，并加入更多自定义选项以提高生产力。——wikipedia

PowerToys是微软官方推出的系统增强工具，完全图形化操作。有很多可选功能，使用起来也较简单。

<u>由于我的需求比较简单，一开始考虑使用PowerToys。但是使用一段时间后发现开了以后有时候会莫名其妙的与我的thinkpad小红点冲突，而且由于软件本身处于Beta阶段，按键有时候会失效。所以最后决定使用AutoHotKey。</u>

## 使用AutoHotKey
1. 到[官网](https://www.autohotkey.com/)下载安装文件。
2. 编写脚本，保存文件后缀名未.ahk。例如以下脚本定义按下```Win+Z```键，打开AutoHotKey官网。具体使用语法，需参考[官网文档](https://wyagd001.github.io/zh-cn/docs/AutoHotkey.htm)。
```
#z::Run https://autohotkey.com  ; Win+Z
```

3. 打开安装后的```Convert .ahk to .exe```，选择脚本源文件，选择生成exe的路径，点击```Convert```，就能在目标路径生成相应的可执行文件。双击就可以后台运行。<u>可以把该文件直接复制到其他电脑打开，这样就可以在任何地方使用同一套快捷键。</u>

![AutoHotKey](/img/使用AutoHotKey映射常用快捷键.png)

##### 开机启动
可以生成一个快捷方式放到```C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp```文件夹下，就可以开机自动启动了。


## 参考脚本
这是按我自己的需求写的脚本，参考了知乎网友nolanzz的回答。

[怎样统一 Windows 和 Mac 上的快捷键使用体验？ - nolanzz的回答 - 知乎](https://www.zhihu.com/question/27564773/answer/1379715851)


```
$!c::
    SendInput {Ctrl Down}{c}{Ctrl Up} ; alt+c 模拟 ctrl+c 复制
Return
$!x::
    SendInput {Ctrl Down}{x}{Ctrl Up} ; alt+x 模拟 ctrl+x 剪切
Return
$!v::
    SendInput {Ctrl Down}{v}{Ctrl Up} ; alt+v 模拟 ctrl+v 保存
Return
$!a::
    SendInput {Ctrl Down}{a}{Ctrl Up} ; alt+a 模拟 ctrl+a 全选
Return
$!s::
    SendInput {Ctrl Down}{s}{Ctrl Up} ; alt+s 模拟 ctrl+s 保存
Return
$!w::
    SendInput {Ctrl Down}{w}{Ctrl Up} ; alt+w 模拟 ctrl+w 关闭窗口
Return
$!z::
    SendInput {Ctrl Down}{z}{Ctrl Up} ; alt+z 模拟 ctrl+z 撤销
Return
$!r::
    SendInput {Ctrl Down}{r}{Ctrl Up} ; alt+r 模拟 ctrl+r 刷新
Return
$!h::
    SendInput {Ctrl Down}{h}{Ctrl Up} ; alt+h 模拟 ctrl+h 替换
Return
$!t::
    SendInput {Ctrl Down}{t}{Ctrl Up} ; alt+t 模拟 ctrl+t 新建标签
Return
$!q::
    SendInput {Alt Down}{F4}{Alt Up} ; alt+q 模拟 alt+f4 关闭窗口
Return
$!f::
    SendInput {Ctrl Down}{f}{Ctrl Up} ; alt+f 模拟 ctrl+f 查找
Return
$!/::
    SendInput {Ctrl Down}{/}{Ctrl Up} ; alt+/ 模拟 ctrl+/ 注释
Return

; 方向键
$!j::
    SendInput {Left}
Return
$!l::
    SendInput {Right}
Return
$!i::
    SendInput {Up}
Return
$!k::
    SendInput {Down}
Return

; 模拟前进后退
$!,::
    SendInput {AltDown}{left}{AltUp}
Return
$!.::
    SendInput {AltDown}{Right}{AltUp}
Return

; alt+shift+n 模拟 ctrl+shift+n，打开无痕模式
$!+n::
SendInput {Ctrl Down}{Shift Down}{n}{Shift Up}{Ctrl Up}
Return

; alt+tab 模拟ctrl+alt+tab, 打开活动窗口（松开不消失）
$!Tab::
    Send {CtrlDown}{AltDown}{Tab}{AltUp}{CtrlUp}
Return
```


更多请查看官方文档：

[快速参考|AutoHotKey](https://wyagd001.github.io/zh-cn/docs/AutoHotkey.htm)