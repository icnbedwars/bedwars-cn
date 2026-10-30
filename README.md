# BedWars-CN for BedWars1058

基于 [BedWars1058](https://github.com/andrei1058/BedWars1058)（GNU GPL-3.0，Andrei Dascălu）的独立分支，适配 Paper 1.21.11，做中文化与功能调整。

上游 BedWars1058 目前未支持 Paper 1.21.11，本分支在源码层面完成了适配，可直接在 Paper 1.21.11 上运行。

## 分支改动

- 中文界面：大厅、对局、胜负结算、商店、计分板均内置简体中文，日志提示也以中文输出。
- 队伍选择：开局前通过箱子选择队伍，支持自动分配与手动选择。
- 自救平台：手持烈焰棒右键，在脚下生成 5×5 史莱姆方块平台，5 秒冷却；死亡复活后重新发放，不会覆盖床。
- 经验模式：可对指定地图开启，商店改为经验支付。
- 商店扩展：默认含下界合金升级、下界合金剑、重锤长矛系列；每个地图可拆分独立的 shop.yml。
- 回城卷轴（3 绿宝石）：右键后 6 秒内不移动，传送到自家。
- 玩家追踪器（10 金锭）：指南针，主手持有时可探测最近的敌人并显示距离。
- 全服喊话 `/hh`：15 秒冷却，点击消息可接受邀请进入房间。
- Admin 房间控制 `/bw admincontrol <房间> ...`：start、end、win（指定队伍胜利）、reset、event（钻石一~三、绿宝石一~三、床被破坏、游戏结束）、destroybed（指定破床），支持中文 Tab 补全。
- 结束房间：将所有玩家传回大厅后进入重启环节。
- 烈焰弹无冷却，速度和爆炸威力可调，伤害半颗心；队伍自动平衡（2 人即可开局）。

## 改名说明

| 项目 | 原版 | 本分支 |
|---|---|---|
| 插件名 | BedWars1058 | BedWars-CN |
| 数据文件夹 | `plugins/BedWars1058/` | `plugins/BedWars-CN/` |
| 主指令 | `/bw` | `/bw`、`/bedwarscn` |
| 全服喊话 | 无 | `/hh` |

首次加载时，若检测到旧的 `plugins/BedWars1058/` 目录，会自动复制到 `plugins/BedWars-CN/`（config、语言、Arenas、商店、tab/ce 模板等），改名不丢配置。

运行要求：Paper 1.21.11，JDK 21。

## 编译

### Linux / macOS

```bash
export JAVA_HOME=/path/to/jdk-21
export PATH=$JAVA_HOME/bin:$PATH
cd sidelib
mvn -s /path/to/settings.xml install -DskipTests -q -o
cd ../bedwars1058
mvn -s /path/to/settings.xml package -pl bedwars-plugin -am -DskipTests -q -o
```

产物：`bedwars1058/bedwars-plugin/target/bedwars-plugin-25.2.jar`，重命名为 `BedWars-CN.jar` 放入 `plugins/`。

### Windows

```bat
set JAVA_HOME=C:\path\to\jdk-21
set PATH=%JAVA_HOME%\bin;%PATH%
cd sidelib
mvn.cmd -s C:\path\to\settings.xml install -DskipTests -q -o
cd ..\bedwars1058
mvn.cmd -s C:\path\to\settings.xml package -pl bedwars-plugin -am -DskipTests -q -o
```

说明：

- 修改过 sidelib 后必须先执行 install，再编插件，否则插件会引用本地仓库里的旧版本。
- 首次构建需要联网拉取依赖（paper-api 1.21.11、spigot-api 等），之后可用 `-o` 离线构建。
- `-s settings.xml` 可省略，需要自定义镜像时再指定。

## 安装

1. 停止服务器。
2. 将 `BedWars-CN.jar` 放入 `plugins/`。
3. 首次启动会自动从 `plugins/BedWars1058/` 迁移配置（若存在）。
4. 重启服务器，确认 `plugins/BedWars-CN/` 下配置完整。

## 上游

- 项目：[BedWars1058](https://github.com/andrei1058/BedWars1058)
- SpigotMC：[BedWars1058 Open Source](https://www.spigotmc.org/resources/bedwars1058-opensource.97320/)
- Wiki：[https://gitlab.com/andrei1058/BedWars1058/wikis](https://gitlab.com/andrei1058/BedWars1058/wikis)

本分支在 GPL-3.0 下发布。
