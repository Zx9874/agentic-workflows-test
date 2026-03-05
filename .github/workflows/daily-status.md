---
# Trigger - when should this workflow run?
on:
  schedule: daily  # 每日自动运行
  workflow_dispatch:  # 手动触发

# AI Engine - 使用 DeepSeek API (OpenAI 兼容)
engine:
  id: codex
  model: deepseek-chat
  env:
    OPENAI_API_BASE: https://api.deepseek.com

# Permissions - 工作流可以访问的权限
permissions:
  contents: read
  issues: read
  pull-requests: read

# Network access
network: defaults

# Outputs - AI 可以使用的输出操作
safe-outputs:
  create-issue:
    max: 1
    title-prefix: "[每日状态] "
    labels: [report, daily-status]

---

# 每日仓库状态报告 (Daily Repository Status)

这是一个自动化工作流，每天生成仓库状态报告。

## 目标 (Goal)

分析仓库活动并创建一份简洁的状态报告。

## 要包含的内容 (What to Include)

请分析以下内容：

1. **Issue 活动** - 新建、关闭、更新的 issue
2. **Pull Request 活动** - 新建、合并、关闭的 PR
3. **代码变更** - 最近的提交活动
4. **待处理事项** - 需要关注的 issue 或 PR

## 报告格式 (Report Format)

创建一个清晰的状态报告，包含：
- 活动摘要
- 重要事项列表
- 建议的下一步行动

## 注意事项 (Notes)

- 使用中文撰写报告
- 保持简洁，突出重点
