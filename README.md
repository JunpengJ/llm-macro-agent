# LLM Macro Analysis Agent

一个基于多Agent协作的RAG系统，用于自动化宏观数据分析。

## 核心特性

- **多Agent协作架构**：搜索、校验、简报、分析四层独立Agent
- **RAG全链路**：从多源数据采集到结构化报告生成
- **六层幻觉防火墙**：工程化抑制LLM幻觉，评分波动约束在±0.2
- **分层记忆机制**：活跃记忆与归档记忆分离，兼顾效率与知识完整
- **动态知识库**：支持规则迭代、版本归档、质量评估闭环
- **异常检测**：自动检测数据异常并触发补充检索

## 架构

```mermaid
flowchart TD
    subgraph 数据层["数据层（Data Layer）"]
        A1[多源数据采集<br/>数据管道层]
        A2[数据清洗与结构化]
        A3[快照 / CSV / 日历]
        A1 --> A2 --> A3
    end

    subgraph Agent层["Agent层（Multi-Agent Layer）"]
        B1[搜索 Agent 集群<br/>多实例并行]
        B2[事实核查 Agent]
        B3[简报 Agent]
        B4[分析 Agent]
    end

    subgraph 校验层["校验层（Validation Layer）"]
        C1[六层幻觉防火墙]
    end

    subgraph 记忆层["记忆层（Memory Layer）"]
        D1[活跃记忆<br/>动态基线]
        D2[归档记忆<br/>历史版本]
    end

    subgraph 调度层["调度层（Scheduler Layer）"]
        E1[调度器]
        E2[异常检测]
        E3[补充搜索]
    end

    A3 --> B1 & B2 & B3
    B1 & B2 & B3 --> B4
    B4 --> B5
    B5 --> C1
    C1 --> B6
    B6 --> D1
    D1 --> E1
    E1 --> E2
    E2 -->|异常| E3
    E3 --> B4
    E2 -->|正常| F[输出报告 / 基线更新]
    D2 -.按需检索.-> B6
    F --> D1
```

## 技术栈

Python · Pandas · Prompt Engineering · Multi-Agent · RAG

## 说明

本仓库仅公开系统架构与通用工具代码。
核心评分规则、数据阈值、权重配比属于项目机密，不在开源范围。