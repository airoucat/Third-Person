# Windows Local Context

本文件只保存这台 Windows 机器上的本地上下文，不作为 shared repo truth。

## 本机仓库

- 本地仓库路径：
  - `C:\Users\xuany\Documents\Third-Person`
- GitHub fork：
  - `https://github.com/airoucat/Third-Person`
- 默认分支：
  - `1.21`

## 本机工具链

- 项目要求 Java 21。
- 当前 Gradle wrapper 使用 `gradle-8.11-bin.zip`。
- wrapper 下载源已切到腾讯 Gradle 镜像：
  - `https://mirrors.cloud.tencent.com/gradle/gradle-8.11-bin.zip`
- graphify 本地自动化入口：
  - `python scripts/dev/setup_graphify_local.py`

## 推荐命令

- 查看版本目标：
  - `Get-Content gradle.properties`
- NeoForge 构建：
  - `.\gradlew.bat :neoforge:build --no-daemon`
- 全量构建：
  - `.\gradlew.bat build --no-daemon`
- 运行 NeoForge client：
  - `.\gradlew.bat :neoforge:runClient --no-daemon`
- 检查 Git 状态：
  - `git status --short --branch`
- 安装 / 修复 graphify 本地自动化：
  - `python scripts/dev/setup_graphify_local.py`
- 手动重建 graphify：
  - `python scripts/dev/setup_graphify_local.py rebuild --reason manual-closeout`

## 下载排错

- 本仓库已在 `settings.gradle` 与 `build.gradle` 中加入国内 Maven 公共镜像，用于减少 Maven Central / Gradle Plugin Portal 下载失败。
- 如果镜像下载仍失败，可以临时走本机代理：

```powershell
$env:JAVA_TOOL_OPTIONS="-Dhttps.proxyHost=127.0.0.1 -Dhttps.proxyPort=7890 -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=7890"
.\gradlew.bat :neoforge:build --no-daemon
```

- 如果 wrapper zip 下载中断，删除残缺文件后重试：
  - `%USERPROFILE%\.gradle\wrapper\dists\gradle-8.11-bin\`

## 本机验证备注

- 构建成功只能说明编译和打包通过。
- 相机、准星、载具和 Sable/Aeronautics 兼容行为必须通过游戏内手工验证记录到 `.third-person-builder/progress.md`。
