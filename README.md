# pr-stack

一个用于演示 [GitHub Stacked Pull Requests](https://docs.github.com/en/pull-requests/get-started/about-stacked-prs) 工作流的示例仓库。

## 项目简介

本仓库展示了如何将大型文档编写任务拆分为一系列小而独立的 Pull Request，每一层 PR 都建立在上一层之上，便于逐层审阅与合并。

### 特性

- 演示 `gh stack` CLI 扩展的完整工作流
- 将 README 文档按逻辑分层提交
- 每个 PR 只包含一个独立、可审阅的变更单元
- 支持底层修改后通过 rebase 自动同步上层分支

## 快速开始

### 前置条件

- [Git](https://git-scm.com/) 2.20+
- [GitHub CLI](https://cli.github.com/) (`gh`) 2.0+，且已完成认证
- `gh stack` 扩展

### 安装 gh stack 扩展

```bash
gh extension install github/gh-stack
```

### 克隆仓库

```bash
git clone https://github.com/jihuayu/pr-stack.git
cd pr-stack
```
