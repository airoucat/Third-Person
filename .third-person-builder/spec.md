# Third-Person Fork Builder Spec Snapshot

## Objective

维护 `airoucat/Third-Person` 的 `1.21` 分支，作为以后默认主分支服务于 `Minecraft 1.21.1 + NeoForge 21.1.145`，并从上游较新分支回填不改变目标版本的通用修复。

## Product Surfaces

- `WF0` Harness + CE workflow bootstrap
- `UPSTREAM1` Upstream fix backport policy
- `BUILD1` Gradle wrapper mirror and build verification
- `RUNTIME1` Camera / crosshair / interaction runtime validation
- `RELEASE1` Fork release preparation

## Hard Constraints

- 默认分支固定为 `1.21`
- 目标 MC 版本固定为 `1.21.1`
- NeoForge 版本固定为 `21.1.145`，除非用户明确要求变更
- current truth 根目录固定为 `docs/current-truth/`
- memory layer 固定为 `.third-person-builder/`
- 共享文档只写 repo-relative 路径，不写机器私有绝对路径
- `passes` 只能在对应验证真实执行后改成 `true`

## Non-Goals

- 不直接合入上游的 MC 版本迁移提交
- 不把 TACZ-LeawindTPS-Compat 的专用兼容层复制进本仓库
- 不在没有验证矩阵时宣称 Aeronautics/Sable 兼容问题已经解决
- 不把本机私有测试实例路径写进 shared docs

## Done Definition

- 当前切片目标、边界和验证入口已经写回 `.third-person-builder/`
- 相关代码、测试或文档改动已落地
- 该切片声明的验证已执行并可复述
- 若构建或游戏内验证未完成，必须在 `progress.md` 写清阻塞原因
