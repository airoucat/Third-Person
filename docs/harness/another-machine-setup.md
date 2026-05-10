# 另一台机器设置指南

用于在另一台机器上接手 `airoucat/Third-Person` fork 的 `1.21` 维护分支。

## Clone

```powershell
git clone https://github.com/airoucat/Third-Person.git
cd Third-Person
git checkout 1.21
```

## Read First

1. `AGENTS.md`
2. 当前机器对应的本地上下文文件
3. `docs/current-truth/README.md`
4. `docs/current-truth/2026-05-10-fork-baseline.md`
5. `docs/harness/third-person-builder.md`
6. `.third-person-builder/`

## Build

```powershell
.\gradlew.bat :neoforge:build --no-daemon
```

如果 Gradle wrapper 下载失败，先确认 `gradle/wrapper/gradle-wrapper.properties` 中的镜像地址是否可访问。

## Graphify

首次进入仓库后安装本地 graphify 自动化：

```powershell
python scripts/dev/setup_graphify_local.py
```

手动重建代码图：

```powershell
python scripts/dev/setup_graphify_local.py rebuild --reason manual-closeout
```
