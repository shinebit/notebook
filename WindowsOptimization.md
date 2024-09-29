## 禁用模块
```batch
::关闭快速启动
powercfg /h off
::禁用索引服务
sc stop WSearch
sc config WSearch start= disabled
::禁用诊断跟踪服务
sc stop DiagTrack
sc config DiagTrack start= disabled
::禁用诊断执行服务，服务主机诊断，系统主机诊断
sc stop diagsvc
sc config diagsvc start= disabled
sc stop WdiServiceHost
sc config WdiServiceHost start= disabled
sc stop WdiSystemHost
sc config WdiSystemHost start= disabled
::禁用错误报告
sc stop WerSvc
sc config WerSvc start= disabled
::禁用脱机文件
sc stop CscService
sc config CscService start= disabled
::删除IE浏览器
Dism /online /Disable-Feature /FeatureName:Internet-Explorer-Optional-amd64 /Remove /NoRestart
::删除媒体功能和Windows Media Player
Dism /online /Disable-Feature /FeatureName:MediaPlayback /Remove /NoRestart
Dism /online /Disable-Feature /FeatureName:WindowsMediaPlayer /Remove /NoRestart
pause
```

## 卸载自带UWP应用
```batch
::卸载3D查看器
powershell "Get-AppxPackage -All *Microsoft3DViewer* | Remove-AppxPackage"
::卸载Cortant
powershell "Get-AppxPackage -All *Microsoft.549981C3F5F10* | Remove-AppxPackage"
::卸载地图
powershell "Get-AppxPackage -All *WindowsMaps* | Remove-AppxPackage"
::卸载电影和电视
powershell "Get-AppxPackage -All *ZuneVideo* | Remove-AppxPackage"
::卸载反馈中心
powershell "Get-AppxPackage -All *WindowsFeedbackHub* | Remove-AppxPackage"
::卸载Groove音乐
powershell "Get-AppxPackage -All *ZuneMusic* | Remove-AppxPackage"
::卸载画图3D
powershell "Get-AppxPackage -All *MSPaint* | Remove-AppxPackage"
::卸载混合现实门户
powershell "Get-AppxPackage -All *MixedReality.Portal* | Remove-AppxPackage"
::卸载获取帮助
powershell "Get-AppxPackage -All *GetHelp* | Remove-AppxPackage"
::卸载录音机
powershell "Get-AppxPackage -All *WindowsSoundRecorder* | Remove-AppxPackage"
::卸载Microsoft Solitaire Collection(微软纸牌合集)
powershell "Get-AppxPackage -All *Microsoft.MicrosoftSolitaireCollection* | Remove-AppxPackage"
::卸载闹钟和时钟
powershell "Get-AppxPackage -All *WindowsAlarms* | Remove-AppxPackage"
::卸载你的手机
powershell "Get-AppxPackage -All *YourPhone* | Remove-AppxPackage"
::卸载OfficeHub
powershell "Get-AppxPackage -All *MicrosoftOfficeHub* | Remove-AppxPackage"
::卸载OneNote
powershell "Get-AppxPackage -All *Office.OneNote* | Remove-AppxPackage"
::卸载人脉
powershell "Get-AppxPackage -All *Microsoft.People* | Remove-AppxPackage"
::卸载邮件和日历
powershell "Get-AppxPackage -All *communicationsapps* | Remove-AppxPackage"
::卸载Skype
powershell "Get-AppxPackage -All *SkypeApp* | Remove-AppxPackage"
::卸载Sticky Notes
powershell "Get-AppxPackage -All *StickyNotes* | Remove-AppxPackage"
::卸载使用技巧
powershell "Get-AppxPackage -All *Getstarted* | Remove-AppxPackage"
::卸载天气
powershell "Get-AppxPackage -All *BingWeather* | Remove-AppxPackage"
::卸载相机
powershell "Get-AppxPackage -All *WindowsCamera* | Remove-AppxPackage"
::卸载照片
powershell "Get-AppxPackage -All *Windows.Photos* | Remove-AppxPackage"
::卸载Wallet（钱包）
powershell "Get-AppxPackage -All *Wallet* | Remove-AppxPackage"
::卸载VP9视频扩展
powershell "Get-AppxPackage -All *Microsoft.VP9VideoExtensions* | Remove-AppxPackage"
::卸载Web媒体扩展
powershell "Get-AppxPackage -All *Microsoft.WebMediaExtensions* | Remove-AppxPackage"
::卸载Webp图像扩展
powershell "Get-AppxPackage -All *Microsoft.WebpImageExtension* | Remove-AppxPackage"
::卸载Clipchamp视频编辑器
powershell "Get-AppxPackage -All *Clipchamp.Clipchamp* | Remove-AppxPackage"
::卸载MicrosoftToDo
powershell "Get-AppxPackage -All *Microsoft.Todos* | Remove-AppxPackage"
::卸载Microsoft咨询
powershell "Get-AppxPackage -All *Microsoft.BingNews* | Remove-AppxPackage"
::卸载快速助手
powershell "Get-AppxPackage -All *MicrosoftCorporationII.QuickAssist* | Remove-AppxPackage"
::卸载小组件
powershell "Get-AppxPackage -All *MicrosoftWindows.Client.WebExperience* | Remove-AppxPackage"
::卸载Outlook
powershell "Get-AppxPackage -All *Microsoft.OutlookForWindows* | Remove-AppxPackage"
::卸载开发人员主页
powershell "Get-AppxPackage -All *Microsoft.Windows.DevHome* | Remove-AppxPackage"
pause
```

## 激活系统
产品密钥：[通用批量许可证密钥](https://docs.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys#generic-volume-license-keys-gvlk)  
win10/11专业版KMS激活
```batch
slmgr /ckms

slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX

slmgr /skms kms.03k.org

slmgr /ato
```

## 任意更改系统更新暂停的时间
```batch
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v FlightSettingsMaxPauseDays /t reg_dword /d 5000 /f
```

## 自带WebDAV Client问题
- 无法连接问题 默认不支持http
    1. 定位注册表 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters`。双击右侧界面中的 `BasicAuthLevel` 条目，将数值数据修改为“`2`”，点击确定后关闭注册表编辑器。
    1. 重启`WebClient`服务
- 解决Windows默认限制为50MB文件大小 超出不允许复制
    1. 定位注册表 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters`找到FileSizeLimitInBytes，双击打开，在打开的设置窗口，选择decimal（十进制）
    1. 修改限制的大小，最大修改为：4294967295（0xffffffff）字节，即4G
    1. 修改好后，再选择hexadecimal（十六进制）

## 网络适配器的网络名称修改
1. 定位注册表 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\`
1. `profiles`文件夹下的不同的网络配置信息(有可能会很多,连过的网络越多,profiles下的文件夹就会越多),查看目录下配置并对`ProfileName`名称进行编辑

## 个性化设置
- Windows10
```batch
::将任务栏中的Cortana调整为 隐藏
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /f /v "SearchboxTaskbarMode" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /f /v "SearchboxTaskbarMode" /t "REG_DWORD" /d "0"
::隐藏“任务视图”按钮
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "ShowTaskViewButton" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "ShowTaskViewButton" /t "REG_DWORD" /d "0"
::隐藏任务栏上的人脉
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\People" /f /v "PeopleBand" /t "REG_DWORD" /d "0"
reg add "HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Explorer" /f /v "HidePeopleBar" /t "REG_DWORD" /d "1"
reg add "HKEY_USERS\.DEFAULT\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\People" /f /v "PeopleBand" /t "REG_DWORD" /d "0"
::打开资源管理器时显示此电脑
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "LaunchTo" /t "REG_DWORD" /d "1"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "LaunchTo" /t "REG_DWORD" /d "1"
::显示所有文件扩展名
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "HideFileExt" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "HideFileExt" /t "REG_DWORD" /d "0"
::显示隐藏的项目
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "Hidden" /t "REG_DWORD" /d "1"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "Hidden" /t "REG_DWORD" /d "1"
::隐藏此电脑中视频、图片、文档、下载、音乐、桌面、3D对象七个文件夹
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{7d83ee9b-2244-4e70-b1f5-5393042af1e4}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{f42ee2d3-909f-4907-8871-4c22fc0bf756}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{0ddd015d-b06c-45d5-8c4c-f59713854639}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{35286a68-3c57-41a1-bbb1-0eae73d76c95}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{a0c69a99-21c8-4671-8703-7934162fcf1d}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{31C0DD25-9439-4F12-BF41-7FF4EDA38722}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide"
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{7d83ee9b-2244-4e70-b1f5-5393042af1e4}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide" /reg:64
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide" /reg:64
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{f42ee2d3-909f-4907-8871-4c22fc0bf756}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide" /reg:64
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{0ddd015d-b06c-45d5-8c4c-f59713854639}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide" /reg:64
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{35286a68-3c57-41a1-bbb1-0eae73d76c95}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide" /reg:64
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{a0c69a99-21c8-4671-8703-7934162fcf1d}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide" /reg:64
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{31C0DD25-9439-4F12-BF41-7FF4EDA38722}\PropertyBag" /f /v "ThisPCPolicy" /t "REG_SZ" /d "Hide" /reg:64
::资源管理器窗口最小化时显示完整路径
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\CabinetState" /f /v "FullPath" /t "REG_DWORD" /d "1"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\CabinetState" /f /v "FullPath" /t "REG_DWORD" /d "1"
::快速访问不显示常用文件夹
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowFrequent" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowFrequent" /t "REG_DWORD" /d "0"
::快速访问不显示最近使用的文件
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowRecent" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowRecent" /t "REG_DWORD" /d "0"
::隐藏资源管理器导航窗口中的库
reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{031E4825-7B94-4dc3-B131-E946B44C8DD5}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2962227469"
reg add "HKEY_CURRENT_USER\Software\Classes\WOW6432Node\CLSID\{031E4825-7B94-4dc3-B131-E946B44C8DD5}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2962227469" /reg:64
::隐藏资源管理器导航窗口中的收藏夹
reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{323CA680-C24D-4099-B94D-446DD2D7249E}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2696937728"
reg add "HKEY_CURRENT_USER\Software\Classes\WOW6432Node\CLSID\{323CA680-C24D-4099-B94D-446DD2D7249E}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2696937728" /reg:64
::隐藏资源管理器导航窗口中的家庭组
reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{B4FB3F98-C1EA-428d-A78A-D1F5659CBA93}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2962489612"
reg add "HKEY_CURRENT_USER\Software\Classes\WOW6432Node\CLSID\{B4FB3F98-C1EA-428d-A78A-D1F5659CBA93}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2962489612" /reg:64
::隐藏资源管理器导航窗口中的网络
reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{F02C1A0D-BE21-4350-88B0-7367FC96EF3C}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2954100836"
reg add "HKEY_CURRENT_USER\Software\Classes\WOW6432Node\CLSID\{F02C1A0D-BE21-4350-88B0-7367FC96EF3C}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2954100836" /reg:64
::隐藏资源管理器导航窗口中的OneDrive
reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "4035969101"
reg add "HKEY_CURRENT_USER\Software\Classes\WOW6432Node\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "4035969101" /reg:64
::隐藏咨询与兴趣
reg add "HKLM\Software\Policies\Microsoft\Windows\Windows Feeds" /f /v "EnableFeeds" /t "REG_DWORD" /d "0"
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Feeds" /f /v "ShellFeedsTaskbarViewMode" /t "REG_DWORD" /d "2"
::Windows10任务栏透明 0-9对应十个透明等级,0为全透明
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "TaskbarAcrylicOpacity" /t "REG_DWORD" /d "0"
::重启资源管理器
taskkill /f /im explorer.exe
start explorer.exe
pause
```
- Windows11
```batch
::打开资源管理器时显示此电脑
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "LaunchTo" /t "REG_DWORD" /d "1"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "LaunchTo" /t "REG_DWORD" /d "1"
::显示所有文件扩展名
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "HideFileExt" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "HideFileExt" /t "REG_DWORD" /d "0"
::显示隐藏的项目
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "Hidden" /t "REG_DWORD" /d "1"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "Hidden" /t "REG_DWORD" /d "1"
::资源管理器窗口最小化时显示完整路径
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\CabinetState" /f /v "FullPath" /t "REG_DWORD" /d "1"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\CabinetState" /f /v "FullPath" /t "REG_DWORD" /d "1"
::快速访问不显示常用文件夹
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowFrequent" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowFrequent" /t "REG_DWORD" /d "0"
::快速访问不显示最近使用的文件
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowRecent" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer" /f /v "ShowRecent" /t "REG_DWORD" /d "0"
::隐藏资源管理器导航窗口中的网络
reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{F02C1A0D-BE21-4350-88B0-7367FC96EF3C}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2954100836"
reg add "HKEY_CURRENT_USER\Software\Classes\WOW6432Node\CLSID\{F02C1A0D-BE21-4350-88B0-7367FC96EF3C}\ShellFolder" /f /v "Attributes" /t "REG_DWORD" /d "2954100836" /reg:64
::使用旧版右键菜单
reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /ve /f
::任务栏隐藏搜索
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /f /v "SearchboxTaskbarMode" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /f /v "SearchboxTaskbarMode" /t "REG_DWORD" /d "0"
::任务栏隐藏任务视图
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "ShowTaskViewButton" /t "REG_DWORD" /d "0"
reg add "HKEY_USERS\.DEFAULT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /f /v "ShowTaskViewButton" /t "REG_DWORD" /d "0"
::重启资源管理器
taskkill /f /im explorer.exe
start explorer.exe
pause
```
