---
name: alphaos-lab
description: AlphaOS 项目入口。当任务涉及 AlphaOS 仓库、其产品/架构/交付文档或 project-spec 时使用，用于定位唯一真源、按文档层加载任务上下文、遵守 Gate 与 CR 纪律。其他项目不要套用。
---

# AlphaOS 工作台

仓库根：`~/Desktop/AlphaOS`（多证券量化研究与投资决策操作系统）。

## 权威顺序

`project-spec/` > `docs/20-design/` > `docs/10-product/prd/` > 其他。冲突时停下并报告，不得自行选择。

## 任务 → 阅读路径（只读所需层，不遍历仓库）

| 任务 | 先读 |
|---|---|
| 产品 / 需求 | `docs/10-product/` |
| 架构 / API / 数据 / 算法 | `docs/20-design/` + `project-spec/` |
| 编码 / CI / 环境 | `docs/30-engineering/` |
| 计划 / Epic / Gate 结论 | `docs/40-delivery/` |
| 运维 / 事故 | `docs/60-operations/` |

阶段与 Gate 现状以 `README.md` 现状表与 `docs/40-delivery/roadmap/` 为准，不要凭记忆假设。

## 写入边界

- 可写：`project-spec/`、`apps/`、`services/`、`packages/`、`database/`、`tests/`、`scripts/`
- 基线只读：`docs/00-project/`、`docs/10-product/`、`docs/20-design/`；变更建议写入 `docs/00-project/changes/`，按 `templates/change-request.md` 格式

## 硬规则

- 阈值来自 Registry、密钥来自密钥管理，禁止硬编码；禁止绕过 PIT 视图读原始数据表（PRD 13.2）
- 禁止修改历史版本对象；禁止复制文档内容形成第二真源，跨文档引用编号或路径
- 禁止绕过 Gate 发布；禁止删除失败与实验记录
- 未运行测试不得提交；提交信息含 `REQ-xxx` 或 `EPIC-xx-Fxx`，基线变更关联 CR 编号
- 新增字段先进 `project-spec/schemas/`，再进代码
