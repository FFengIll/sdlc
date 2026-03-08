# SDLC Skills System v2 - Simplified Design

**Date**: 2026-03-08
**Version**: 2.0 (Simplified)
**Status**: Design

## Overview

A streamlined SDLC skill system with a single entry point that dispatches to focused phase skills, sharing foundational capabilities.

## Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                         SDLC SKILL SYSTEM v2                                     │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │                              /sdlc                                      │   │
│  │                         (Single Entry Point)                            │   │
│  └───────────────────────────────────────┬─────────────────────────────────┘   │
│                                          │                                     │
│          ┌───────────────────────────────┼───────────────────────────────┐     │
│          │                               │                               │     │
│          ▼                               ▼                               ▼     │
│  ┌──────────────┐              ┌──────────────┐              ┌──────────────┐  │
│  │  research    │              │     spec     │              │      cr      │  │
│  │  调研        │              │   规格/设计   │              │  代码审查     │  │
│  └──────────────┘              └──────────────┘              └──────────────┘  │
│                                                                                 │
│  ┌──────────────┐              ┌──────────────┐              ┌──────────────┐  │
│  │    test      │              │    debug     │              │   commit     │  │
│  │   测试        │              │    调试       │              │   提交        │  │
│  └──────────────┘              └──────────────┘              └──────────────┘  │
│                                                                                 │
│  ┌──────────────┐              ┌──────────────┐              ┌──────────────┐  │
│  │     pr       │              │  validate    │              │   secure     │  │
│  │  PR管理       │              │   验证        │              │   安全        │  │
│  └──────────────┘              └──────────────┘              └──────────────┘  │
│                                                                                 │
├─────────────────────────────────────────────────────────────────────────────────┤
│                              SHARED FOUNDATION                                  │
│  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐                                   │
│  │  doc   │  │ pencil │  │ cache  │  │  git   │                                   │
│  │ 文档    │  │ 画图   │  │ 缓存    │  │ 版本控制│                                   │
│  └────────┘  └────────┘  └────────┘  └────────┘                                   │
└─────────────────────────────────────────────────────────────────────────────────┘

USAGE:
/sdlc research  - 调研新技术/方案
/sdlc spec      - 编写规格/设计文档
/sdlc cr        - 代码审查
/sdlc test      - 测试相关
/sdlc debug     - 调试问题
/sdlc commit    - 提交代码
/sdlc pr        - PR 管理
/sdlc validate  - 验证（lint/typecheck/等）
/sdlc secure    - 安全检查

FOUNDATION SKILLS (可独立调用):
/doc      - 文档生成/管理
/pencil   - 画图/设计
/cache    - 缓存管理
/git      - Git 操作
```

## System Structure

```
skills/
├── README.md                    # 系统说明
├── sdlc.md                      # 主入口技能
├── phases/                      # SDLC 阶段技能
│   ├── research.md             # 调研
│   ├── spec.md                 # 规格/设计
│   ├── cr.md                   # 代码审查 (Code Review)
│   ├── test.md                 # 测试
│   ├── debug.md                # 调试
│   ├── commit.md               # 提交
│   ├── pr.md                   # PR 管理
│   ├── validate.md             # 验证
│   └── secure.md               # 安全
└── foundation/                  # 基础技能
    ├── doc.md                  # 文档
    ├── pencil.md               # 画图 (已有)
    ├── cache.md                # 缓存
    └── git.md                  # Git 操作
```

## Phase Skills

### `/sdlc research`
**用途**: 技术调研、方案评估

**功能**:
- 调研新技术/库/框架
- 比较不同方案
- 生成调研文档

**使用**:
```
/sdlc research <调研主题>
```

**输出**: `./docs/research/{date}-{topic}.md`

**依赖**: `doc`, `cache`

---

### `/sdlc spec`
**用途**: 编写规格说明、设计文档

**功能**:
- 需求分析
- 架构设计
- API 设计
- 数据结构设计

**使用**:
```
/sdlc spec <功能/主题>
```

**输出**: `./docs/spec/{date}-{title}.md`

**依赖**: `doc`, `pencil`, `cache`

---

### `/sdlc cr` (Code Review)
**用途**: 代码审查

**功能**:
- 审查代码变更
- 检查最佳实践
- 提供改进建议
- 安全审查

**使用**:
```
/sdlc cr [文件/分支/PR]
```

**依赖**: `doc`, `cache`

---

### `/sdlc test`
**用途**: 测试相关

**功能**:
- 生成测试用例
- 运行测试
- 分析覆盖率
- 测试策略建议

**使用**:
```
/sdlc test [测试类型/文件]
```

**依赖**: `cache`

**子命令**:
- `/sdlc test unit` - 单元测试
- `/sdlc test integ` - 集成测试
- `/sdlc test e2e` - 端到端测试
- `/sdlc test coverage` - 覆盖率分析

---

### `/sdlc debug`
**用途**: 调试问题

**功能**:
- 分析错误
- 定位问题
- 提供修复建议
- 生成调试步骤

**使用**:
```
/sdlc debug <问题描述/错误日志>
```

**依赖**: `cache`

---

### `/sdlc commit`
**用途**: 提交代码

**功能**:
- 生成 commit message
- 检查变更
- 提交前验证
- 执行提交

**使用**:
```
/sdlc commit [提交信息]
```

**依赖**: `git`, `validate`

---

### `/sdlc pr`
**用途**: PR 管理

**功能**:
- 创建 PR
- 生成 PR 描述
- 审查协调
- 合并管理

**使用**:
```
/sdlc pr [create|review|merge]
```

**依赖**: `doc`, `git`, `cache`

---

### `/sdlc validate`
**用途**: 验证代码质量

**功能**:
- Lint 检查
- 类型检查
- 格式化
- 静态分析

**使用**:
```
/sdlc validate [检查类型]
```

**子命令**:
- `/sdlc validate lint` - Lint 检查
- `/sdlc validate type` - 类型检查
- `/sdlc validate format` - 格式化
- `/sdlc validate all` - 全部检查

---

### `/sdlc secure`
**用途**: 安全检查

**功能**:
- 安全漏洞扫描
- 依赖检查
- 密钥检测
- 安全最佳实践

**使用**:
```
/sdlc secure [检查范围]
```

## Foundation Skills

### `/doc`
**用途**: 文档生成和管理

**功能**:
- 生成 API 文档
- 创建架构图
- 维护 CHANGELOG
- 生成用户指南

**使用**:
```
/doc <文档类型> <主题>
```

**输出**: `./docs/{category}/{date}-{name}.md`

**类别**:
- `api` - API 文档
- `arch` - 架构文档
- `guide` - 使用指南
- `changelog` - 变更日志

---

### `/pencil` (已有)
**用途**: 画图、UI 设计

**功能**:
- 线框图
- 流程图
- 架构图
- UI 设计

**使用**:
```
/pencil <设计描述>
```

**输出**: `./docs/pencil/{date}-{name}.md`

---

### `/cache`
**用途**: 缓存管理，留存知识

**功能**:
- 缓存项目结构理解
- 存储架构决策
- 检索缓存上下文
- 减少重复分析

**使用**:
```
/cache <操作> [key]
```

**操作**:
- `save` - 保存缓存
- `load` - 加载缓存
- `clear` - 清除缓存
- `list` - 列出缓存

**输出**: `./docs/arch/{date}-arch.md`

**缓存内容**:
- 项目结构
- 架构决策
- 技术栈信息
- 配置模式
- 依赖关系

---

### `/git`
**用途**: Git 操作辅助

**功能**:
- 分支管理
- 提交生成
- 合并协助
- 冲突解决

**使用**:
```
/git <操作> [参数]
```

**操作**:
- `branch` - 分支操作
- `commit` - 提交操作
- `merge` - 合并操作
- `status` - 状态查询

## Workflows

### 完整功能开发流程
```
/sdlc research → 研究方案
    ↓
/sdlc spec     → 编写规格
    ↓
/pencil        → 设计 UI/架构
    ↓
[开发代码]
    ↓
/sdlc validate → 验证代码
    ↓
/sdlc test     → 运行测试
    ↓
/sdlc secure   → 安全检查
    ↓
/sdlc commit   → 提交代码
    ↓
/sdlc pr       → 创建 PR
    ↓
/sdlc cr       → 代码审查
    ↓
/git merge     → 合并代码
```

### Bug 修复流程
```
/sdlc debug    → 定位问题
    ↓
[修复代码]
    ↓
/sdlc validate → 验证修复
    ↓
/sdlc test     → 回归测试
    ↓
/sdlc commit   → 提交修复
```

### 重构流程
```
/sdlc cr       → 审查现有代码
    ↓
/sdlc spec     → 设计重构方案
    ↓
[重构代码]
    ↓
/sdlc validate → 验证重构
    ↓
/sdlc test     → 运行测试
    ↓
/sdlc commit   → 提交重构
```

## Cache 策略

### 缓存内容
```markdown
<!-- ./docs/arch/{date}-arch.md -->
# 项目架构缓存

## 项目结构
- 目录树
- 模块组织
- 文件分布

## 技术栈
- 前端框架
- 后端框架
- 数据库
- 工具链

## 架构决策
- 设计模式
- 数据流
- 依赖关系

## 配置模式
- 构建配置
- 部署配置
- 环境变量

## 代码约定
- 命名规范
- 文件组织
- 注释风格
```

### 缓存使用
1. **自动缓存**: 每次使用 `/sdlc` 技能时自动更新缓存
2. **手动缓存**: 使用 `/cache save` 保存特定信息
3. **缓存命中**: 技能优先从缓存读取上下文
4. **缓存失效**: 检测到重大变更时更新缓存

## 与现有技能的映射

| 现有技能 | 新技能 | 说明 |
|---------|--------|------|
| `/spec` | `/sdlc spec` | 移入 phases/ |
| `/pencil` | `/pencil` | 保留，移入 foundation/ |
| `/pr` | `/sdlc pr` | 移入 phases/ |
| `/codereview` | `/sdlc cr` | 移入 phases/，简化名称 |
| `/refactor` | `/sdlc spec` + `/sdlc cr` | 拆分 |
| `/git-commit` | `/sdlc commit` | 移入 phases/ |
| `/discuss` | `/sdlc research` | 合并 |
| `/research` | `/sdlc research` | 移入 phases/ |
| `/codeclean` | `/sdlc validate` | 移入 phases/ |
| `/test-go` | `/sdlc test` | 合并到通用测试 |
| `/refactor-go` | `/sdlc cr` | 合并 |
| `/review-branch` | `/sdlc cr` | 合并 |
| `/review-refactor` | `/sdlc cr` | 合并 |
| `/specreview` | `/sdlc cr` | 合并 |
| `/new-command` | - | 保留独立 |
| `/update-arch` | `/cache` | 重命名并移入 foundation/ |
| `/optimize-go-test` | `/sdlc test` | 合并 |

## 实现优先级

### Phase 1: 核心 (Week 1)
1. `/sdlc` - 主入口
2. `/cache` - 缓存系统
3. `/doc` - 文档系统
4. `/sdlc spec` - 规格

### Phase 2: 开发流程 (Week 2)
5. `/sdlc research` - 调研
6. `/sdlc validate` - 验证
7. `/sdlc test` - 测试
8. `/sdlc commit` - 提交

### Phase 3: 审查流程 (Week 3)
9. `/sdlc cr` - 代码审查
10. `/sdlc pr` - PR 管理
11. `/sdlc debug` - 调试
12. `/sdlc secure` - 安全

### Phase 4: 整合 (Week 4)
13. 迁移现有技能
14. 文档完善
15. 测试和优化

## 优势

1. **简洁**: 只有 9 个阶段技能 + 4 个基础技能 = 13 个总技能
2. **统一**: 单一入口 `/sdlc`，易于记忆和使用
3. **灵活**: 每个技能可独立使用，也可组合工作流
4. **可扩展**: 未来可添加新阶段而不影响现有结构
5. **缓存共享**: 所有技能共享缓存，提高效率
