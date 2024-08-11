# VSCode
`settings.json`
```jsonc
{
    //在没有从上一次会话中恢复出信息的情况下启动时不打开任何编辑器(默认启动时显示欢迎页)
    "workbench.startupEditor": "none",
    //取消显示命令中心(搜索栏)
    "window.commandCenter": false,
    //自动保存
    "files.autoSave": "afterDelay",
    //打开文件时猜测字符集编码
    "files.autoGuessEncoding": true,
    //光标动画样式
    "editor.cursorBlinking": "smooth",
    //编辑器动画
    "editor.smoothScrolling": true,
    //启用平滑插入动画
    "editor.cursorSmoothCaretAnimation": "on",
    //自动换行
    "editor.wordWrap": "on",
    //不启用工作区信任
    "security.workspace.trust.enabled": false
}
```


# mpv
`portable_config` `\` `mpv.conf`
```conf
#开启缓存
cache=yes
#最大缓存大小（KiB或MiB）
demuxer-max-bytes=64MiB
#用内存而不是磁盘缓存
cache-on-disk=no

#无边框
border=no
#设置默认打开的窗口大小、位置(1280x720、居中）
geometry=1280x720+50%+50%

#自动加载外部字幕文件方式。（fuzzy加载同文件夹含有视频文件名的字幕文件）
sub-auto=fuzzy

#启动默认音量
volume=100
#程序最大音量[100,1000]
volume-max=100
```
