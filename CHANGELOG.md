# Changelog

本项目所有显著变更都会记录在此文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，
版本号遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)。

## [Unreleased]

### Added
- 完整仓库脚手架：README / LICENSE / CONTRIBUTING / CHANGELOG
- 文档：`docs/usage.md`、`docs/templates.md`、`docs/best-practices.md`
- 示例计划：`examples/order-refactor/`（含 4 个步骤文件 + 启动器 + 状态表）
- 辅助脚本：`scripts/check-task-status.sh` / `scripts/check-task-status.ps1` / `scripts/init-plan.sh`
- GitHub Issue / PR 模板

## [1.0.0] - 2026-06-23

### Added
- 初始发布 `SKILL.md` —— 完整的分步处理规则与模板
- 强制规则：每个 session 启动前读取 `task-status.md`；全部完成时直接告知结束
- 强制规则：目标目录必须经用户确认，且必须位于项目根目录内
- 强制规则：每个步骤文件必须可被独立 session 直接执行
- 强制规则：session 结束前同步更新 `next-session.md` 与 `task-status.md`

[Unreleased]: https://github.com/wangxi83/step-processing/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/wangxi83/step-processing/releases/tag/v1.0.0
