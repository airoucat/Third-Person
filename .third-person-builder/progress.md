# Third-Person Fork Builder Progress

## 2026-05-10

- `start`
  - 目标：把 `airoucat/Third-Person` 的 `1.21` 分支配置成以后默认的 1.21.1 维护主线，并配置 repo-local harness。
  - 现状：fork 默认分支已切到 `1.21`；本地 `1.21` 已回填一组上游通用修复；Gradle wrapper 之前从 `services.gradle.org` 下载 `gradle-8.11-bin.zip` 超时。
  - 策略：把 wrapper 分发包下载源改成国内镜像；新增 `AGENTS.md`、`AGENTS.win.md`、`docs/current-truth/`、`docs/harness/`、`.third-person-builder/`。

- `decision`
  - 默认分支：`1.21`
  - 目标版本：`Minecraft 1.21.1`
  - NeoForge：`21.1.145`
  - 上游同步策略：只 cherry-pick 不改变目标版本的修复，不直接合入版本迁移提交。

- `verification`
  - `gradle/wrapper/gradle-wrapper.properties` 已改为腾讯 Gradle 镜像，并把 `networkTimeout` 调整为 `60000`。
  - `.\gradlew.bat :neoforge:build --no-daemon` 已能从镜像完整下载 Gradle 8.11。
  - 首次构建仍失败在 Maven classpath 依赖解析：部分通用依赖误走 Forge Maven，Fabric Maven 出现 TLS handshake 中断。
  - 处理：在 `settings.gradle` 和 `build.gradle` 中加入国内 Maven 公共镜像，并把 Forge Maven 放到更靠后的位置。

- `blocked`
  - 第二次执行 `.\gradlew.bat :neoforge:build --no-daemon` 后，构建运行超过 25 分钟仍未自然结束。
  - 已停止本次 `Third-Person` 构建产生的 Gradle wrapper / Gradle 8.11 daemon 进程。
  - 当前可确认：Gradle wrapper 镜像配置有效；完整 NeoForge build 尚未通过，后续需要继续排查 Maven 依赖下载或 Gradle 配置阶段卡住的具体依赖。

## 2026-05-11

- `correction`
  - 用户指出 harness 不完整，缺少 graphify。
  - 结论：上一轮只迁移了 `harness + ce`，没有迁移 TACZ 项目中的 `graphify` 自动化；这不是完整 harness。

- `start GRAPH1`
  - 目标：补齐 repo-local graphify setup、Git hooks、Codex 本地 hook、ignore 规则、AGENTS 入口和 harness 状态。
  - 来源：参考 `TACZ-LeawindTPS-Compat` 中的 `scripts/dev/setup_graphify_local.py`、`.githooks/`、`scripts/dev/codex_graphify_pre_tool_hook.ps1`。

- `complete GRAPH1`
  - 已新增：`.githooks/`、`scripts/dev/setup_graphify_local.py`、`scripts/dev/codex_graphify_pre_tool_hook.ps1`。
  - 已更新：`AGENTS.md`、`AGENTS.win.md`、`docs/harness/`、`docs/current-truth/`、`.third-person-builder/`、`.gitignore`。
  - 已验证：
    - `python scripts/dev/setup_graphify_local.py`
    - `git config --local --get core.hooksPath`
    - `graphify-out/GRAPH_REPORT.md` 生成成功
  - 首轮 graphify 输出：`655 nodes, 1255 edges, 38 communities`。
