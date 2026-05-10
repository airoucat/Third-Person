# Third-Person Fork Current Truth

本目录是当前 fork 的 shared current truth 根目录。

## 一句话定义

本仓库是 `Leawind's Third Person` 的非官方维护 fork，当前默认维护 `Minecraft 1.21.1 + NeoForge 21.1.145` 的 `1.21` 分支，并从上游较新分支回填不改变目标版本的通用修复。

## 当前 source map

- 公共入口与初始化：
  - `common/src/main/java/com/github/leawind/thirdperson/ThirdPerson.java`
  - `common/src/main/java/com/github/leawind/thirdperson/ThirdPersonConstants.java`
  - `common/src/main/java/com/github/leawind/thirdperson/ThirdPersonKeys.java`
- 相机核心：
  - `common/src/main/java/com/github/leawind/thirdperson/core/CameraAgent.java`
  - `common/src/main/java/com/github/leawind/thirdperson/core/EntityAgent.java`
- 事件与状态：
  - `common/src/main/java/com/github/leawind/thirdperson/event/`
  - `common/src/main/java/com/github/leawind/thirdperson/config/`
- client mixin：
  - `common/src/main/java/com/github/leawind/thirdperson/mixin/CameraMixin.java`
  - `common/src/main/java/com/github/leawind/thirdperson/mixin/EntityMixin.java`
  - `common/src/main/java/com/github/leawind/thirdperson/mixin/LocalPlayerMixin.java`
- 平台入口：
  - `fabric/src/main/java/com/github/leawind/thirdperson/fabric/ThirdPersonFabric.java`
  - `neoforge/src/main/java/com/github/leawind/thirdperson/neoforge/ThirdPersonNeoForge.java`
  - `neoforge/src/main/java/com/github/leawind/thirdperson/neoforge/ThirdPersonNeoForgeClient.java`
- 构建与版本：
  - `gradle.properties`
  - `build.gradle`
  - `settings.gradle`
  - `gradle/wrapper/gradle-wrapper.properties`

## 默认阅读顺序

1. `docs/current-truth/README.md`
2. `docs/current-truth/2026-05-10-fork-baseline.md`
3. `docs/harness/third-person-builder.md`
4. `.third-person-builder/spec.md`
5. `.third-person-builder/feature_list.json`
6. `.third-person-builder/sprint_plan.json`
7. `.third-person-builder/progress.md`

## 当前已知边界

- `1.21` 是 fork 的默认主分支。
- `minecraft_version` 必须保持 `1.21.1`，除非用户明确要求迁移主版本。
- `minecraft_version_max` 必须保持 `1.21.1`，避免误发布成更高版本兼容。
- `neoforge_version` 当前保持 `21.1.145`。
- 上游 `1.21.11` 可作为修复来源，但版本迁移提交不能直接合入。
- 这个 fork 的目标是支撑 1.21.1 整合包环境，不是替代上游所有最新版本发布线。
