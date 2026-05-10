# Third-Person Fork Builder Harness

这是把 `harness + ce` 工作流落到 `airoucat/Third-Person` fork 后的默认说明。

目标不是引入一组松散技能，而是把 repo 级执行协议固定下来：

- `harness` 负责项目状态、完成定义和进度同步
- `ce` 负责默认的规划、实现、审查执行
- `.third-person-builder/` 负责保存当前实施状态

## Related Docs

- `docs/current-truth/README.md`
  - 当前 fork 的 shared current truth 与 source map
- `docs/current-truth/2026-05-10-fork-baseline.md`
  - 1.21.1 维护分支的基线约束

## Concept Mapping

| 模板概念 | 本仓库落地 |
| --- | --- |
| `planner` | 默认由 `ce:plan` 执行；确认当前维护目标、上游回填边界和验证入口 |
| `generator` | 默认由 `ce:work` 执行；只实现当前切片范围内的代码、测试和必要文档 |
| `evaluator` | 默认由 `ce:review` 执行；验证行为是否诚实、是否引入版本漂移或平台回归 |
| `sync` | 同步更新 `.third-person-builder/feature_list.json`、`sprint_plan.json`、`progress.md` |
| `memory layer` | `.third-person-builder/`，是 repo 内当前实施状态的默认记忆层 |

## Memory Layer

根目录下的 `.third-person-builder/` 是默认项目实施记忆层：

- `spec.md`
  - 项目目标、硬约束、非目标、完成定义
- `feature_list.json`
  - 顶层工作单元、状态与 `passes`
- `sprint_plan.json`
  - 当前 sprint、依赖、退出标准、验证方式
- `progress.md`
  - 时间线、阻塞、验证结果、重要决策

## Default Execution Loop

1. `Planner`
   - 先读 `docs/current-truth/README.md`
   - 再读 `.third-person-builder/spec.md`、`feature_list.json`、`sprint_plan.json`、`progress.md`
   - 确认当前要推进的是上游回填、构建修复、运行时兼容，还是发布准备
2. `Generator`
   - 只在当前切片范围内写代码、测试、脚本和必要文档
   - 不把无关的版本迁移、大型重构或新兼容想法偷渡进当前切片
3. `Evaluator`
   - 对照当前切片声明的验证入口做审查
   - 优先找 MC/loader 版本漂移、Fabric/NeoForge 单侧损坏、mixin 注入漂移和验证不诚实
4. `Sync`
   - 同步更新 `.third-person-builder/feature_list.json`
   - 同步更新 `.third-person-builder/sprint_plan.json`
   - 向 `.third-person-builder/progress.md` 追加记录

## Repo-Specific Rules

- current truth 根目录始终是 `docs/current-truth/`
- 记忆层始终是 `.third-person-builder/`
- 当前默认主分支是 `1.21`
- 当前目标版本是 `Minecraft 1.21.1 + NeoForge 21.1.145`
- 从上游同步时，优先 cherry-pick 小而明确的修复提交
- 不合入会改变目标 MC 版本的上游迁移提交，除非用户明确要求

## Validation Expectations

常见验证入口：

- `git diff --check`
- `.\gradlew.bat :neoforge:build --no-daemon`
- `.\gradlew.bat build --no-daemon`
- `.\gradlew.bat :neoforge:runClient --no-daemon`
- 针对当前变更的手工游戏内验证

`passes` 只能在对应验证实际执行并通过后改成 `true`。

## Definition Of Done

一个切片只有同时满足下面条件才算完成：

- 当前范围内的代码、测试、文档已经落地
- 已执行该切片声明的验证，并且结果可复述
- `.third-person-builder/feature_list.json` 与 `.third-person-builder/sprint_plan.json` 状态一致
- `.third-person-builder/progress.md` 记录了开始、结论和风险
