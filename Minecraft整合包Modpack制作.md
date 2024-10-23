### CurseForge 托管包
- 特征：以 Zip 压缩包发布，压缩包内第一层有`overrides`文件夹和`manifest.json`、`modlist.html`两个文件。（可能有少部分包不包含`modlist.html`）  
- 结构：
```
Modpack.zip
├─ manifest.json
├─ modlist.html
└─ overrides/
       ├─ config/
       ├─ mods/
       └─ resourcepacks/
```
- 配置文件模板：`manifest.json`
```json
{
  "minecraft": {
    "version": "[游戏版本]",
    "modLoaders": [
      {
        "id": "[mod加载器类型]-[mod加载器版本]",
        "primary": true
      }
    ]
  },
  "manifestType": "minecraftModpack",
  "manifestVersion": 1,
  "name": "[整合包名称]",
  "version": "1.0.0",
  "author": "[整合包作者]",
  "files": [],
  "overrides": "overrides"
}
```
### Modrinth 托管包
- 特征：以 mrpack 格式或 Zip 压缩包发布，包内第一层有`overrides`文件夹和`modrinth.index.json`文件。
- 结构：
```
Modpack.mrpack
├─ modrinth.index.json
└─ overrides/
       ├─ config/
       ├─ mods/
       └─ resourcepacks/
```
- 配置文件模板：`modrinth.index.json`
```json
{
    "formatVersion": 1,
    "game": "minecraft",
    "versionId": "1.0.0",
    "name": "[整合包名称]",
    "files": [],
    "dependencies": {
        "[mod加载器类型]": "[mod加载器版本]",
        "minecraft": "[游戏版本]"
    }
}
```
