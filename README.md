# SandGraphX

**SandGraphX** 基于对于environment subsets的抽象（SandBox）和最终的优化目标（Optimization Goal）的优化框架，该框架会基于SandBox Workflow Graph进行计算。

## 🌟 核心特性

- **官方MCP集成**：基于 Anthropic 的官方 MCP Python SDK
- **沙盒环境**：遵循 Game24bootcamp 模式的标准化任务环境
- **工作流图**：支持复杂 LLM-Sandbox交互的 DAG 执行引擎
- **标准化通信**：使用官方 MCP 协议进行 LLM-Sandbox通信
- **多种使用场景**：从单一沙盒执行到复杂多阶段工作流
- **生态系统兼容**：与 Claude Desktop、Cursor、Windsurf 等 MCP 客户端兼容
- **动态工作流引擎**：支持复杂的DAG（有向无环图）工作流，实现多节点协作
- **智能状态管理**：每个节点维护独立的状态，支持动态更新和状态追踪
- **多智能体协作**：支持多个LLM智能体之间的协作与通信
- **沙盒环境集成**：提供标准化的沙盒环境，用于任务执行和验证
- **资源管理系统**：内置资源（能量、令牌、时间、知识）管理机制
- **自适应决策**：支持基于历史信息和当前状态的智能决策
- **可扩展架构**：易于添加新的节点类型和功能模块

## 📁 文件结构

```
SandGraph/
├── sandgraph/                    # 核心包目录
│   ├── core/                     # 核心功能模块
│   │   ├── workflow.py          # 基础工作流实现
│   │   ├── sg_workflow.py       # SandGraph工作流实现
│   │   ├── dag_manager.py       # DAG图管理
│   │   ├── llm_interface.py     # LLM接口
│   │   ├── sandbox.py           # 沙盒基础类
│   │   ├── rl_framework.py      # 强化学习框架
│   │   └── rl_algorithms.py     # 强化学习算法
│   ├── sandbox_implementations.py # 沙盒实现
│   └── examples.py              # 示例代码
├── sg_workflow_demo.py          # 工作流演示
├── rl_demo.py                   # 强化学习演示
└── setup.py                     # 安装配置
```

## 🏗️ 系统架构

```
┌─────────────────────────────────────────────────────────┐
│                      SandGraph Core                     │
├─────────────┬─────────────┬─────────────┬─────────────┤
│  Workflow   │   State     │   Resource  │   Decision  │
│   Engine    │  Manager    │  Manager    │   Engine    │
└──────┬──────┴──────┬──────┴──────┬──────┴──────┬──────┘
       │             │             │             │
       ▼             ▼             ▼             ▼
┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│   LLM Nodes │ │ Sandbox     │ │ Resource    │ │ Decision    │
│             │ │ Nodes       │ │ Nodes       │ │ Nodes       │
└─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘
```

## 🎯 主要功能

### 1. 动态工作流系统
- 支持复杂的多节点工作流
- 节点间状态传递和依赖管理
- 灵活的工作流定义和执行

### 2. 智能节点类型
- **分析节点**：负责数据分析和模式识别
- **策略节点**：制定行动策略和计划
- **评估节点**：风险评估和质量控制
- **资源节点**：资源分配和优化
- **决策节点**：最终决策和执行

### 3. 状态管理系统
- 节点状态追踪
- 历史信息记录
- 状态更新和验证
- 置信度评分

### 4. 资源管理
- 能量管理
- 令牌控制
- 时间限制
- 知识储备

## 📦 安装

```bash
# 基础安装
pip install sandgraph

# 开发安装
git clone https://github.com/NoakLiu/sandgraph.git
cd sandgraph
pip install -e ".[dev]"
```

## 🚀 快速开始

### 1. 创建简单工作流

```python
from sandgraph import SG_Workflow, NodeType, WorkflowMode
from sandgraph.core.llm_interface import create_shared_llm_manager
from sandgraph.sandbox_implementations import Game24Sandbox

# 1. 创建LLM管理器
llm_manager = create_shared_llm_manager("demo_llm")

# 2. 创建工作流
workflow = SG_Workflow("demo_workflow", WorkflowMode.TRADITIONAL, llm_manager)

# 3. 添加节点
# 3.1 添加输入节点
workflow.add_node(NodeType.INPUT, "start")

# 3.2 添加LLM分析节点
workflow.add_node(NodeType.LLM, "analyzer", {
    "role": "分析器",
    "reasoning_type": "analytical"
})

# 3.3 添加沙盒节点
workflow.add_node(NodeType.SANDBOX, "game_sandbox", {
    "sandbox": Game24Sandbox(),
    "max_visits": 3
})

# 3.4 添加输出节点
workflow.add_node(NodeType.OUTPUT, "end")

# 4. 添加边
workflow.add_edge("start", "analyzer")
workflow.add_edge("analyzer", "game_sandbox")
workflow.add_edge("game_sandbox", "end")

# 5. 执行工作流
result = workflow.execute_full_workflow(max_steps=10)
```

### 2. 标准输出结果

```
============================================================
 传统工作流模式演示
============================================================

创建传统工作流图: demo_workflow
模式: TRADITIONAL
节点数: 4
边数: 3

----------------------------------------
 初始游戏状态
----------------------------------------
资源: {'energy': 100, 'tokens': 50, 'time': 300, 'knowledge': 100}
可执行节点: ['start']

----------------------------------------
 执行工作流
----------------------------------------
执行完成:
- 总步骤: 4
- 执行时间: 2.35秒
- 最终得分: 0.85
- 剩余资源: {'energy': 75, 'tokens': 35, 'time': 285, 'knowledge': 95}
- 完成节点数: 4

----------------------------------------
 节点执行详情
----------------------------------------
1. start节点:
   - 状态: 完成
   - 执行时间: 0.05秒
   - 资源消耗: {'energy': 5, 'tokens': 2}

2. analyzer节点:
   - 状态: 完成
   - 执行时间: 0.85秒
   - 资源消耗: {'energy': 10, 'tokens': 8}
   - 置信度: 0.92

3. game_sandbox节点:
   - 状态: 完成
   - 执行时间: 1.20秒
   - 资源消耗: {'energy': 15, 'tokens': 10}
   - 得分: 0.85

4. end节点:
   - 状态: 完成
   - 执行时间: 0.25秒
   - 资源消耗: {'energy': 5, 'tokens': 5}
```

### 3. 创建动态游戏系统

```python
from sandgraph import create_dynamic_game_graph

# 创建动态游戏图
game_graph = create_dynamic_game_graph(llm_manager)

# 执行游戏
result = game_graph.execute()
```

### 4. 量化交易系统
- 市场数据分析
- 交易策略生成
- 实时交易执行
- 风险控制
- 投资组合管理

#### 4.1 交易环境集成
SandGraph 提供了与 Trading Gym 和 Backtrader 的集成，支持：
- 实时市场数据获取（Yahoo Finance, Alpaca）
- 交易执行和回测
- 投资组合管理
- 风险控制
- 性能评估

使用示例：
```python
from sandgraph import SG_Workflow, NodeType, WorkflowMode
from sandgraph.core.llm_interface import create_shared_llm_manager
from sandgraph.sandbox_implementations import BacktraderSandbox
from datetime import datetime, timedelta

# 创建LLM管理器
llm_manager = create_shared_llm_manager("trading_llm")

# 创建工作流
workflow = SG_Workflow("trading_workflow", WorkflowMode.TRADITIONAL, llm_manager)

# 添加交易执行节点
workflow.add_node(NodeType.SANDBOX, "trading_executor", {
    "sandbox": BacktraderSandbox(
        initial_cash=100000.0,
        commission=0.001,
        data_source="yahoo",
        symbols=["AAPL", "GOOGL", "MSFT", "AMZN"],
        start_date=(datetime.now() - timedelta(days=365)).strftime("%Y-%m-%d"),
        end_date=datetime.now().strftime("%Y-%m-%d")
    ),
    "max_visits": 5
})

# 执行工作流
result = workflow.execute_full_workflow(max_steps=10)
```

#### 4.2 交易功能
- **市场数据**：支持实时和历史市场数据获取
- **交易执行**：支持市价单、限价单等交易类型
- **投资组合**：支持多资产组合管理
- **风险控制**：支持止损、仓位控制等风险管理
- **性能评估**：支持夏普比率、最大回撤等指标计算

#### 4.3 数据源支持
- Yahoo Finance
- Alpaca Trading API
- 自定义数据源

#### 4.4 交易策略
- 趋势跟踪
- 均值回归
- 套利策略
- 机器学习策略

#### 4.5 Backtrader 集成
SandGraph 集成了 Backtrader 框架，提供以下功能：
- **历史数据回测**：支持多周期、多资产回测
- **实时交易**：支持实时市场数据交易
- **多策略组合**：支持多个交易策略的组合
- **性能分析**：内置多种性能分析指标
  - 夏普比率
  - 最大回撤
  - 年化收益率
  - 交易统计
- **可视化**：支持交易结果可视化
  - 资产曲线
  - 交易点位
  - 技术指标
  - 性能指标

使用 Backtrader 的示例：
```python
from sandgraph.sandbox_implementations import BacktraderSandbox

# 创建 Backtrader 沙盒
sandbox = BacktraderSandbox(
    initial_cash=100000.0,
    commission=0.001,
    data_source="yahoo",
    symbols=["AAPL", "GOOGL", "MSFT", "AMZN"],
    start_date="2023-01-01",
    end_date="2023-12-31"
)

# 执行回测
result = sandbox.execute_backtest()
print(f"回测结果：\n{result}")
```

#### 4.6 命令行使用
SandGraph 提供了命令行工具来运行交易演示：

1. 使用 Backtrader 策略（默认）：
```bash
python trading_demo.py
```

2. 使用 TradingGym 策略：
```bash
python trading_demo.py --strategy trading_gym
```

3. 查看帮助信息：
```bash
python trading_demo.py --help
```

输出：
```
usage: trading_demo.py [-h] [--strategy {trading_gym,backtrader}]

SandGraph 交易环境演示

options:
  -h, --help            显示帮助信息并退出
  --strategy {trading_gym,backtrader}
                        选择交易策略类型 (trading_gym 或 backtrader)
```

4. 开发环境安装和运行：
```bash
# 安装开发版本
pip install -e ".[dev]"

# 运行演示
python trading_demo.py --strategy backtrader  # 使用 Backtrader
# 或
python trading_demo.py --strategy trading_gym  # 使用 TradingGym
```

#### 4.7 性能指标
- **收益指标**
  - 总收益率
  - 年化收益率
  - 月度收益率
  - 胜率
- **风险指标**
  - 夏普比率
  - 最大回撤
  - 波动率
  - 信息比率
- **交易指标**
  - 交易次数
  - 平均持仓时间
  - 盈亏比
  - 手续费成本

## 📚 示例场景

### 1. 游戏分析系统
- 市场模式识别
- 策略规划
- 风险评估
- 资源优化

### 2. 多智能体协作
- 任务分解
- 并行执行
- 结果聚合
- 质量评估

### 3. 动态决策系统
- 状态分析
- 策略生成
- 风险评估
- 决策执行

### 4. 量化交易系统
- 市场数据分析
- 交易策略生成
- 实时交易执行
- 风险控制
- 投资组合管理

#### 4.1 交易环境集成
SandGraph 提供了与 Trading Gym 和 Backtrader 的集成，支持：
- 实时市场数据获取（Yahoo Finance, Alpaca）
- 交易执行和回测
- 投资组合管理
- 风险控制
- 性能评估

使用示例：
```python
from sandgraph import SG_Workflow, NodeType, WorkflowMode
from sandgraph.core.llm_interface import create_shared_llm_manager
from sandgraph.sandbox_implementations import BacktraderSandbox
from datetime import datetime, timedelta

# 创建LLM管理器
llm_manager = create_shared_llm_manager("trading_llm")

# 创建工作流
workflow = SG_Workflow("trading_workflow", WorkflowMode.TRADITIONAL, llm_manager)

# 添加交易执行节点
workflow.add_node(NodeType.SANDBOX, "trading_executor", {
    "sandbox": BacktraderSandbox(
        initial_cash=100000.0,
        commission=0.001,
        data_source="yahoo",
        symbols=["AAPL", "GOOGL", "MSFT", "AMZN"],
        start_date=(datetime.now() - timedelta(days=365)).strftime("%Y-%m-%d"),
        end_date=datetime.now().strftime("%Y-%m-%d")
    ),
    "max_visits": 5
})

# 执行工作流
result = workflow.execute_full_workflow(max_steps=10)
```

#### 4.2 交易功能
- **市场数据**：支持实时和历史市场数据获取
- **交易执行**：支持市价单、限价单等交易类型
- **投资组合**：支持多资产组合管理
- **风险控制**：支持止损、仓位控制等风险管理
- **性能评估**：支持夏普比率、最大回撤等指标计算

#### 4.3 数据源支持
- Yahoo Finance
- Alpaca Trading API
- 自定义数据源

#### 4.4 交易策略
- 趋势跟踪
- 均值回归
- 套利策略
- 机器学习策略

#### 4.5 Backtrader 集成
SandGraph 集成了 Backtrader 框架，提供以下功能：
- **历史数据回测**：支持多周期、多资产回测
- **实时交易**：支持实时市场数据交易
- **多策略组合**：支持多个交易策略的组合
- **性能分析**：内置多种性能分析指标
  - 夏普比率
  - 最大回撤
  - 年化收益率
  - 交易统计
- **可视化**：支持交易结果可视化
  - 资产曲线
  - 交易点位
  - 技术指标
  - 性能指标

使用 Backtrader 的示例：
```python
from sandgraph.sandbox_implementations import BacktraderSandbox

# 创建 Backtrader 沙盒
sandbox = BacktraderSandbox(
    initial_cash=100000.0,
    commission=0.001,
    data_source="yahoo",
    symbols=["AAPL", "GOOGL", "MSFT", "AMZN"],
    start_date="2023-01-01",
    end_date="2023-12-31"
)

# 执行回测
result = sandbox.execute_backtest()
print(f"回测结果：\n{result}")
```

#### 4.6 性能指标
- **收益指标**
  - 总收益率
  - 年化收益率
  - 月度收益率
  - 胜率
- **风险指标**
  - 夏普比率
  - 最大回撤
  - 波动率
  - 信息比率
- **交易指标**
  - 交易次数
  - 平均持仓时间
  - 盈亏比
  - 手续费成本

## 🔧 开发指南

### 添加新节点类型
1. 定义节点属性
2. 实现状态更新逻辑
3. 注册到工作流系统

### 自定义工作流
1. 定义节点结构
2. 设置节点依赖
3. 配置执行参数

## 📝 贡献指南

欢迎提交 Pull Requests 和 Issues！请确保：
1. 代码符合项目规范
2. 添加适当的测试
3. 更新相关文档

## 📄 许可证

MIT License
## 🤝 联系方式

- 邮件联系 - dong.liu.dl2367@yale.edu
