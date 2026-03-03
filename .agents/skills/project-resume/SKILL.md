---
name: project-resume
description: 恢复项目上下文 — 新对话开始时自动追上项目进度，避免"智力回退"
---

# 项目上下文恢复技能

## 触发条件

**自动触发**：当新对话开始且用户的 workspace 包含此项目时，**不需要用户说任何特定指令**，直接在回答用户的第一个问题之前，静默执行以下步骤获取上下文。不要把恢复上下文的过程展示给用户，直接带着上下文去干活。

## 执行步骤

### 1. 读取项目记忆

// turbo
读取 workspace 根目录的 `MEMORY.md`：
```
view_file MEMORY.md
```

如果 `MEMORY.md` 不存在，跳到第 2 步后**主动创建一个**。

### 2. 扫描目录结构

// turbo
用 `list_dir` 扫描 workspace 根目录和各子目录，了解当前文件结构：
```
list_dir <workspace_root>
```

与 `MEMORY.md` 中的记录做对比，识别对话外的变化（新增/删除/重命名的文件）。

### 3. 检查用户当前焦点

从 `ADDITIONAL_METADATA` 中获取：
- 当前打开的文件（Active Document）
- 光标位置（Cursor line）
- 其他打开的文件（Other open documents）

这些表明用户正在关注的区域。

### 4. 静默就绪

**不要**做汇报，直接带着上下文回应用户的问题。只有当 MEMORY.md 与目录结构明显不一致时，才简要提醒用户。

## 注意事项

- **不要**长篇大论重复项目背景
- **不要**列出所有文件
- **优先**读 `MEMORY.md`，它是最可靠的上下文来源
