---
name: research-and-reuse
description: Advisory heuristic to prioritize open-source patterns and proactive web/GitHub research. Encourages looking for existing solutions and battle-tested recipes during complex designs or sticky errors, while fully respecting model autonomy for clear tasks.
---

# Skill: research-and-reuse

Maintain an engineering mindset of **"Standing on the Shoulders of Giants"**: Favor battle-tested open-source solutions and external intelligence when tackling architectural complexity or stubborn friction.

---

## Core Mindset (启发式原则)

1. **Reuse Over Reinvention (复用优于自研)**: 
   - 社区通常已经踩过绝大多数并发、重试、流式传输或状态机的暗坑。在构思复杂逻辑前，优先评估是否有轻量、成熟的开源方案或经典模式可直接参考。
2. **Search as a Lever, Not a Chore (搜索是高杠杆杠杆)**:
   - 遇到不熟悉的框架怪癖或二次报错时，网络搜索与 GitHub Issues 往往是获取 Root Cause 最省力的路径，远快于主观推理。
3. **Respect Autonomy (保持自主与克制)**:
   - **无需无意义搜索**：对于上下文清晰、已有充分把控的标准开发与局部调整，直接执行，绝不为了“合规”而浪费时间检索。

---

## High-Value Reflex Points (强提醒触发时机)

在做决策时，若感知到以下信号，请主动激活“搜索/查阅开源”的反射神经：

### 1. 复杂/通用子系统设计前 (Before Designing Complex Subsystems)
- **信号**：你正准备手写超过几十行逻辑来实现一个通用的底层能力（例如：任务并发限制、指数退避重试、复杂表单校验器、多标签页状态同步、文件分片断点续传等）。
- **启发提问**：*“这个轮子社区是不是已有经过千锤百炼的标准库或官方最佳实践（如 `p-limit`, `p-retry` 等）？”*
- **推荐动作**：简要调研是否有工业级解决方案，优先复用或借鉴其代码结构。

### 2. 调试遇到二次摩擦 (Encountering Debugging Friction)
- **信号**：第一次修复尝试失败，或者遇到了框架特有的生命周期/状态机怪异现象（如 Next.js 偶发脱水报错、构建工具神秘退出、隐式类型冲突）。
- **启发提问**：*“我是不是在凭经验臆测？社区 Issue 里是否早有现成结论与变通方案（Workaround）？”*
- **推荐动作**：提取关键报错特征或场景关键词，在 GitHub Issues、Discussions 或 StackOverflow 中快速检索验证。

### 3. 依赖快速迭代的前沿技术 (Fast-Moving Ecosystems)
- **信号**：涉及大版本更迭频繁的库（如最新版本的前端框架、AI/LLM SDK、新版构建工具）。
- **启发提问**：*“我脑中的 API 签名与设计模式是否可能已经过时或被废弃（Deprecated）？”*
- **推荐动作**：快速查阅官方最新文档或版本发布说明（Changelog），防范知识库过时引发的幻觉。

---

## Tactical Search Query Formulas (高精准度检索参考)

当需要调用搜索工具时，推荐构造信息密度高、工程师维度的精准查询，而非口语化搜索：

- **排查疑难报错**：`"[Exact Error Message]"` `[Framework]` `site:github.com`
- **寻找参考实现**：`best practice [Tech Stack] [Feature]` OR `github repo [Feature] [Language]`
- **查找知名方案**：`how does [Known Library] implement [Mechanism]`

---

## Pragmatic Reuse Guidelines (务实复用准则)

- **避免过度引入依赖**：如果成熟方案很轻量（或核心逻辑仅几行），可直接汲取其核心算法与设计思想，手写适配，无需无脑引入庞大的依赖包。
- **注明灵感出处**：若采纳了开源项目的设计模式或官方 Issue 的规避策略，在说明中一笔带过其出处（例如：“*参考了社区针对该 Issue 的标准绕行方案*”），保持工程透明度。
