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

## Stacked PRs 工作流

本仓库的 README 文档正是通过 Stacked PRs 逐层构建的。以下是核心命令：

### 1. 初始化 Stack

```bash
gh stack init readme/intro
```

创建第一个分支并建立 stack 追踪。

### 2. 编写并提交

```bash
git add README.md
git commit -m "Add project introduction"
```

### 3. 添加下一层分支

```bash
gh stack add readme/getting-started
# 继续编写并提交...
```

### 4. 推送并创建 PR

```bash
gh stack submit --auto
```

每个 PR 的 base 分支会自动设置为 stack 中的上一层，PR 之间会链接为一个 Stack。

### 5. 查看 Stack 状态

```bash
gh stack view --json
```

### Stack 结构

```
main (trunk)
 └── readme/intro              → PR #1 (base: main)
  └── readme/getting-started   → PR #2 (base: readme/intro)
   └── readme/stacked-prs-guide → PR #3 (base: readme/getting-started)
    └── readme/contributing    → PR #4 (base: readme/stacked-prs-guide)
```

### 同步与合并

```bash
# 同步远程变更并 rebase
gh stack sync

# 合并整个 stack（从底层到顶层）
gh stack merge --yes
```

更多详情请参阅 [Stacked PRs Quickstart](https://docs.github.com/en/pull-requests/get-started/stacked-prs-quickstart)。

## 贡献指南

欢迎通过 Stacked PRs 方式为本仓库贡献文档改进。

### 贡献流程

1. Fork 本仓库并克隆到本地
2. 使用 `gh stack init` 创建你的 stack
3. 按逻辑分层编写变更，每层一个分支
4. 运行 `gh stack submit --auto` 创建 PR stack
5. 从底层 PR 开始逐层审阅与合并

### 分支命名建议

- 使用描述性分支名，如 `readme/intro`、`docs/api-guide`
- 每个分支只包含一个逻辑单元的变更
- 底层分支放基础内容，上层分支放依赖底层的扩展内容

### 修改底层分支

如果在高层分支工作时发现需要修改底层内容：

```bash
gh stack down          # 导航到底层分支
# 修改并提交
gh stack rebase --upstack  # 将变更 rebase 到上层
gh stack top           # 回到顶层继续工作
```

## 许可证

本项目采用 MIT 许可证。
