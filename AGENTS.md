# Third-Person Fork 协作入口

本文件是任何新对话进入本仓库时的默认入口。

如果当前机器是 Windows，读完本文件后继续阅读 `AGENTS.win.md`。`AGENTS.win.md` 保存这台 Windows 机器上的本地环境、构建命令和测试实例信息。

## 当前仓库状态

- 当前仓库是 `Leawind's Third Person` 的非官方 fork。
- GitHub fork：`airoucat/Third-Person`
- 默认维护分支：`1.21`
- 当前目标版本：`Minecraft 1.21.1 + NeoForge 21.1.145`，同时保留 Fabric 构建面。
- 上游参考仓库：`Leawind/Third-Person`
- 当前策略：从上游新版本回填通用修复，但不直接合入会把目标版本迁到 `1.21.4`、`1.21.9`、`1.21.11` 的提交。

## 新对话默认阅读顺序

1. `AGENTS.md`
2. 若当前机器是 Windows，再读 `AGENTS.win.md`
3. `docs/current-truth/README.md`
4. `docs/current-truth/2026-05-10-fork-baseline.md`
5. `docs/harness/third-person-builder.md`
6. `.third-person-builder/spec.md`
7. `.third-person-builder/feature_list.json`
8. `.third-person-builder/sprint_plan.json`
9. `.third-person-builder/progress.md`

## 默认工作流

- 本仓库默认采用 `harness + ce + graphify` 作为 repo-level workflow。
- repo 内记忆层固定在 `.third-person-builder/`。
- 三段式默认映射：
  - `Planner -> ce:plan`
  - `Generator -> ce:work`
  - `Evaluator -> ce:review`
- 每次开始、完成、返工或阻塞一个工作切片时，都向 `.third-person-builder/progress.md` 追加记录。
- 只要本轮改动涉及代码文件，在宣告完成前必须执行：
  - `python scripts/dev/setup_graphify_local.py rebuild --reason manual-closeout`
- 没有实际验证前，不要把 `.third-person-builder/feature_list.json` 里的 `passes` 改成 `true`。

## Graphify 本地自动化

- `graphify-out/` 是本地生成物，不提交到 Git。
- 仓库内版本化 hooks 位于 `.githooks/`，用于在本机的 `commit / checkout / merge / rebase` 后自动重建代码图。
- 每台新机器 clone 或首次进入仓库后，只需要执行一次：
  - `python scripts/dev/setup_graphify_local.py`
- 这一步会：
  - 自动安装或复用本机 `graphifyy`
  - 配置本地 `git config core.hooksPath .githooks`
  - 补齐本机 `.codex/hooks.json`
  - 在本地尚无 `graphify-out/graph.json` 时自动生成首轮代码图
- 手动重建入口统一使用：
  - `python scripts/dev/setup_graphify_local.py rebuild --reason manual-closeout`

## 工作规则

- 新文档默认使用中文。
- 共享文档只写 repo-relative 路径，不写机器私有绝对路径。
- 机器相关路径只写到 `AGENTS.win.md`。
- 涉及版本迁移时，先确认 `gradle.properties` 中的 `minecraft_version`、`minecraft_version_max`、`neoforge_version` 是否仍符合 1.21.1 维护目标。
- 涉及相机、准星、人物渲染、输入或 pick 行为时，先读 `docs/current-truth/README.md` 的 source map，再决定改哪个模块。
- `graphify-out/` 只作为上下文加速，不替代 `docs/current-truth/` 或 `.third-person-builder/`。

## 快速路由

- “继续维护 1.21.1 主线”
  先读 `docs/current-truth/2026-05-10-fork-baseline.md` 和 `.third-person-builder/`。

- “从上游同步最新修复”
  先比对 `upstream/1.21.11` 与当前 `1.21`，只挑选不改变 MC/loader 目标版本的修复。

- “构建 NeoForge jar”
  在 Windows 上使用 `.\gradlew.bat :neoforge:build --no-daemon`。

- “构建全部平台”
  使用 `.\gradlew.bat build --no-daemon`，但需要确认 Fabric 和 NeoForge 两侧依赖都能下载。

- “重建 graphify”
  在仓库根目录执行 `python scripts/dev/setup_graphify_local.py rebuild --reason manual-closeout`。

## graphify

This project has a graphify knowledge graph at `graphify-out/`.

Rules:
- Before answering architecture or codebase questions, read `graphify-out/GRAPH_REPORT.md` for god nodes and community structure.
- If `graphify-out/wiki/index.md` exists, navigate it instead of reading raw files.
- Treat graphify as a context accelerator, not the source of truth over `docs/current-truth/` or `.third-person-builder/`.
- After modifying code files in this session, run `python scripts/dev/setup_graphify_local.py rebuild --reason manual-closeout`.
