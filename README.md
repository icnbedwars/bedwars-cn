# BadWars-CN for BedWars1058

**BadWars-CN** 是基于 [BedWars1058](https://github.com/andrei1058/BedWars1058)（Andrei Dascălu 开源项目，GNU GPL-3.0）的独立汉化增强分支，专为 **Paper 1.21.11** 适配，并包含大量面向中文玩家/服务器的功能与修复。

> 上游 BedWars1058 官方版本目前**尚未支持 Paper 1.21.11**（官方仍在开发 1.21 支持），本分支在源码层面完成了 1.21.11 的 NMS/API 适配，可正常在 Paper 1.21.11 上运行。

---

## 一、分支特色

- **全面汉化**：内置中文语言文件（zh_cn），涵盖大厅、游戏内、胜利/失败/游戏结束、商店、计分板等全部界面；日志提示也尽量中文。
- **原生队伍选择器**：开赛倒计时前给玩家箱子选队（自动分配/手动选择）。
- **自救平台**：任意烈焰棒右键即可在脚下生成 5×5 史莱姆方块平台（5 秒冷却、死亡复活后再次发放），支持掉落虚空自救，不会覆盖床方块。
- **经验模式**：可在指定地图启用经验模式，商店用经验支付。
- **自定义商店**：默认含下界合金升级/下界合金剑/重锤长矛系等（可按地图拆分 shop.yml 单独配置）。
- **回城卷轴**（3 绿宝石）：右键 6 秒不移动传送回自家。
- **玩家追踪器**（10 金锭）：指南针，主手探测最近敌人并显示距离。
- **全服喊话** `/hh`：15 秒冷却，点击消息可接受邀请进入房间。
- **Admin 房间控制** `/bw admincontrol <房间> ...`：start / end / win（指定队伍胜利）/ reset / event（环节跳转：钻石一~三、绿宝石一~三、床被破坏、游戏结束）/ destroybed（指定破床），中文 Tab 补全。
- **结束房间**：一键将所有玩家传送回大厅并进入重启环节。
- 烈焰弹无冷却、更快、爆炸威力可调、伤害半颗心；智能平衡选队（2 人也能开局，队伍人数尽量均衡且不小于 4 人）。

---

## 二、改名说明（独立分支）

| 项目 | 原版 | BadWars-CN 分支 |
|---|---|---|
| 插件名 | BedWars1058 | **BadWars-CN** |
| 数据文件夹 | `plugins/BedWars1058/` | **`plugins/BadWars-CN/`** |
| 主指令 | `/bw` | `/bw` 与 **`/badwarscn`**（等价，均可用） |
| 全服喊话 | — | `/hh` |

> **数据自动迁移**：首次加载时若发现旧的 `plugins/BedWars1058/` 数据目录，会自动完整复制到 `plugins/BadWars-CN/`（config、语言、Arenas 地图、商店、tab/ce 模板等），升级改名不丢任何配置。

> 服务器版本：Paper **1.21.11**；Java **21**（运行与编译均需 JDK 21）。

---

## 三、编译命令

### Linux / macOS

```bash
# 1. 编译 sidelib（sidebar 基础库），必须先装到本地 Maven 仓库
export JAVA_HOME=/path/to/jdk-21
export PATH=$JAVA_HOME/bin:$PATH
cd sidelib
mvn -s /path/to/settings.xml install -DskipTests -q -o

# 2. 编译并打包插件
cd ../bedwars1058
mvn -s /path/to/settings.xml package -pl bedwars-plugin -am -DskipTests -q -o
```

产物：`bedwars1058/bedwars-plugin/target/bedwars-plugin-25.2.jar`，重命名为 `BadWars-CN.jar` 放入服务器 `plugins/` 目录。

### Windows（PowerShell / CMD）

```bat
:: 1. 编译 sidelib
set JAVA_HOME=C:\path\to\jdk-21
set PATH=%JAVA_HOME%\bin;%PATH%
cd sidelib
mvn.cmd -s C:\path\to\settings.xml install -DskipTests -q -o

:: 2. 编译并打包插件
cd ..\bedwars1058
mvn.cmd -s C:\path\to\settings.xml package -pl bedwars-plugin -am -DskipTests -q -o
```

> 说明：
> - `-o` 表示离线构建；首次构建需要联网拉取依赖（paper-api 1.21.11、spigot-api、sidebar 各版本等），或直接复制本机 `~/.m2` 仓库。
> - `-s settings.xml` 为可选，指向你的 Maven settings；无特殊镜像需求可省略 `-s`。
> - 修改了 sidelib 代码后，**必须先执行第 1 步**再编插件，否则插件会用旧的本地仓库版本。

---

## 四、安装与升级

1. 停止服务器。
2. 将 `BadWars-CN.jar` 放入 `plugins/`。
3. 首次启动会自动从 `plugins/BedWars1058/` 迁移配置（如存在）。
4. 重启服务器，检查 `plugins/BadWars-CN/` 目录已生成且配置完整。

---

## 五、上游

- 上游项目：[BedWars1058](https://github.com/andrei1058/BedWars1058)（GNU GPL-3.0，Andrei Dascălu）
- 上游 SpigotMC：[BedWars1058 Open Source](https://www.spigotmc.org/resources/bedwars1058-opensource.97320/)
- 上游 Wiki：[https://gitlab.com/andrei1058/BedWars1058/wikis](https://gitlab.com/andrei1058/BedWars1058/wikis)

本分支在 GPL-3.0 许可下发布，欢迎为本分支贡献代码或提出 Issue。
