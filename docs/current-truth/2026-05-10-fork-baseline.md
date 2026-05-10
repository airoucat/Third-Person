# 2026-05-10 Fork 基线快照

## Objective

维护 `airoucat/Third-Person` 的 `1.21` 分支，使其作为以后默认主分支服务于 `Minecraft 1.21.1 + NeoForge 21.1.145`，同时从上游新版本回填不改变版本目标的修复。

## Product Surfaces

- Gradle / Architectury / Loom 构建配置
- Fabric 和 NeoForge 平台入口
- Leawind 第三人称相机、准星、pick、玩家透明和输入行为
- 与下游兼容模组联调时需要稳定依赖的公共行为
- repo-level harness 记忆层

## Hard Constraints

- 默认分支固定为 `1.21`。
- 不直接合入把项目迁移到 `1.21.4`、`1.21.9`、`1.21.11` 的提交。
- 回填上游修复时必须保留 `gradle.properties` 中的 1.21.1 版本目标。
- 共享文档只写 repo-relative 路径。
- `passes` 只能在对应验证真实执行后改成 `true`。

## Current Backport Baseline

本 fork 已从上游较新分支回填一组通用修复和构建维护提交，当前 HEAD 保持在 `1.21` 分支上。

已保留的目标版本：

```properties
minecraft_version = 1.21.1
minecraft_version_min = 1.21
minecraft_version_max = 1.21.1
neoforge_version = 21.1.145
```

## Verification Expectations

- 代码级检查：
  - `git diff --check`
  - 冲突标记扫描
- 构建检查：
  - `.\gradlew.bat :neoforge:build --no-daemon`
  - 必要时再执行 `.\gradlew.bat build --no-daemon`
- 下载源：
  - Gradle wrapper 使用腾讯 Gradle 镜像
  - Maven 依赖优先尝试国内公共镜像，再回退到 Fabric / Architectury / Forge 等专用仓库
- 游戏内检查：
  - F5 第三人称切换
  - 相机平滑与透明度
  - 常规方块交互、实体交互、弓/枪/工具类右键
  - 与 TACZ-LeawindTPS-Compat、Aeronautics/Sable 场景联调

## Non-Goals

- 不在本 fork 中直接复制 TACZ-LeawindTPS-Compat 的专用兼容代码。
- 不把上游最新 MC 版本路线作为默认发布目标。
- 不把本机私有测试实例路径写入 shared current truth。
