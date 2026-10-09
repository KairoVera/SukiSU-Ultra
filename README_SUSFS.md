# SUSFS 集成说明

## 概述

SUSFS (Suspicious File System) 是一个内核级安全功能，需要与 GKI 内核源码集成。

## 当前架构

- **SukiSU-Ultra/kernel/**: KSU 内核模块代码（不含 SUSFS）
- **AndroidGKI**: 负责 GKI 内核构建 + SUSFS 补丁应用

## 如何使用

### 1. 在 AndroidGKI 中启用 SUSFS

```bash
# 触发构建时指定 SUSFS 选项
gh workflow run main.yml -f use_susfs=true
```

### 2. 使用 custom-main 分支

custom-main 是 SukiSU-Ultra 的新架构分支，支持：
- 标准 Kbuild 系统
- 模块化设计（core/, feature/, hook/）
- 与 AndroidGKI 配合使用 SUSFS

## SUSFS 补丁位置

SUSFS 补丁通过 submodule 管理：
- 路径: `kernel/susfs-patches/`
- 源: https://gitlab.com/simonpunk/susfs4ksu

## 版本说明

- **builtin 分支**: 旧架构，已内置 SUSFS
- **main/custom-main**: 新架构，SUSFS 由 AndroidGKI 集成

## 注意事项

1. 不要直接对 custom-main 应用 SUSFS 补丁（架构不兼容）
2. 如需使用 SUSFS，请在 AndroidGKI 中构建
3. Manager APK 版本来自 main 分支，内核来自 builtin 或 custom-main
