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
