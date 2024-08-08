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
reg add “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings” /v FlightSettingsMaxPauseDays /t reg_dword /d 5000 /f
```

## 自带WebDAV Client问题
- 无法连接问题 默认不支持http
1. 定位注册表 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters`。双击右侧界面中的 `BasicAuthLevel` 条目，将数值数据修改为“`2`”，点击确定后关闭注册表编辑器。
1. 重启`WebClient`服务
- 解决Windows默认限制为50MB文件大小 超出不允许复制
1. 定位注册表 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters`找到FileSizeLimitInBytes，双击打开，在打开的设置窗口，选择decimal（十进制）
1. 修改限制的大小，最大修改为：4294967295（0xffffffff）字节，即4G
1. 修改好后，再选择hexadecimal（十六进制）

## 修复图标变白
```batch
del /S /Q %HOMEPATH%\AppData\Local\IconCache.db
```

## 网络适配器的网络名称修改
定位注册表 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\`
profiles文件夹下的不同的网络配置信息(有可能会很多,连过的网络越多,profiles下的文件夹就会越多)
查看目录下配置并对ProfileName名称进行编辑

## 开启自动登录功能
```batch
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\PasswordLess\Device" /f /v "DevicePasswordLessBuildVersion" /t "REG_DWORD" /d "0"
```
运行`netplwiz`配置

## 修复jar文件无法直接打开
```batch
reg add HKEY_CLASSES_ROOT\Applications\javaw.exe\shell\open\command /f /d "\"[java路径]\bin\javaw.exe\" -jar \"%1\""
```
`[java路径]`为java安装路径，右键属性更改默认打开方式为javaw.exe

## 以管理员身份运行或提权需进行身份验证
```batch
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /f /v "ConsentPromptBehaviorAdmin" /t "REG_DWORD" /d "3"
```
