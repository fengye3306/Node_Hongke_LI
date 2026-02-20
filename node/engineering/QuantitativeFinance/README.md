## 量化金融

### AI给出的学习路线


下面给你一份 工业级 AI量化工程师成长路线图。
我按真实量化团队（hedge fund / prop trading / quant tech）的工程流程设计，重点是：能做系统、能做研究、能上线策略，而不是只会跑模型。
考虑到你有较强软件开发背景（Qt/C++、系统开发经验明显），这份路线图会偏 工程落地 + AI建模，而不是纯金融理论。

🧭 AI量化工程师成长路线图（工业级）
🎯 最终能力目标（行业标准）

你完成后应该具备：

✔ 构建量化研究平台
✔ 设计特征工程流水线
✔ 实现AI策略训练系统
✔ 实现Walk-forward回测
✔ 接交易API实盘
✔ 实现风险控制与监控

🧱 一、整体技术架构（工业视角）

真实AI量化系统结构：

```text
┌─────────────────────┐
│      Data Layer      │ 数据采集 / 清洗 / 存储
├─────────────────────┤
│  Feature Pipeline    │ 因子工程 / 滚动窗口
├─────────────────────┤
│  ML Training Engine  │ 模型训练 / CV / 调参
├─────────────────────┤
│  Backtest Engine     │ 事件驱动回测
├─────────────────────┤
│ Execution Engine     │ 下单 / OMS
├─────────────────────┤
│ Risk Engine          │ 风控
└─────────────────────┘
```


你的目标不是写一个策略，而是写 系统。

🧠 二、阶段化成长路线（强执行版）


> 阶段1：量化基础工程（2~4周）

* 会写回测
* 理解时间序列
* 避免未来函数


技术：
* Python（必须）
* pandas / numpy / polars
* matplotlib
* vectorbt ⭐⭐⭐⭐⭐

项目（必须做）：
项目1：动量策略回测系统

功能：
读取数据
生成信号
计算收益
计算Sharpe
计算回撤


你要自己实现：
rolling window
shift
resample



> 阶段2：AI策略研发（1~2个月）

目标：
做真正的AI策略（不是玩具）

核心技术：
LightGBM ⭐⭐⭐⭐⭐
XGBoost
sklearn pipeline

你要实现：
Walk-forward validation
时间序列CV
标签延迟


项目：

项目2：AI预测next-day return

流程：

特征生成
训练模型
预测信号
回测


特征例子：

RSI
Momentum
Volatility
Rolling mean
Cross asset return

> 阶段3：工业级研究框架（2~3个月）

目标：

做一个研究平台（像mini hedge fund）


模块：

Data Layer

parquet存储

多资产

时间对齐

Feature Engine

实现：

Feature DAG
缓存机制
自动更新

Training Engine

实现：

多模型训练
参数搜索
模型版本管理

Backtest Engine

必须支持：

事件驱动
滑点模型
手续费
延迟
仓位管理

> 阶段4：实盘系统（高级工程）

目标：

自动交易系统


模块：

Execution Engine
订单管理 OMS
成交回报
重试机制
风控拦截


接口建议：

IBKR

Alpaca

Binance

FIX

Risk Engine

实现：

最大仓位
最大回撤
波动率缩放
止损

🧪 三、AI量化核心算法路线（行业真实）
第一梯队（最赚钱）
LightGBM
XGBoost
Logistic Regression

第二梯队
Random Forest
Linear Factor Model
Kalman Filter
HMM

第三梯队（研究）
LSTM
Transformer
Temporal Fusion Transformer
RL Trading


现实：

80%机构不用深度学习

🛠 四、工业级工具链（真实量化团队用）
数据
Parquet
Arrow
DuckDB ⭐⭐⭐⭐⭐
kdb+（机构）

研究框架
vectorbt ⭐⭐⭐⭐⭐
Qlib（微软）
Backtrader

ML
lightgbm
optuna ⭐⭐⭐⭐⭐
mlflow

基础设施
Docker
Airflow
Ray
Dask

🧩 五、必须做的工业级项目（含含金量）
⭐ 项目A：AI多因子平台

功能：

因子库
因子IC分析
自动选因子
模型训练
组合优化

⭐ 项目B：Walk-forward自动训练系统

实现：

滚动训练
自动部署模型
性能监控

⭐ 项目C：完整交易系统

结构：

research/
execution/
risk/
data/
monitor/

📈 六、成长阶段 vs 行业水平
阶段	能力	年薪级别（US）
初级	会回测	80k
中级	会AI策略	120k
高级	能做研究平台	180k
资深	能做交易系统	250k+
🚨 七、工业级避坑指南（极其重要）
❌ Random Train/Test

必须：

Walk-forward

❌ K线图像喂CNN

几乎没机构这么做。

❌ 不建模交易成本

必须模拟：

slippage
latency
spread

❌ 追求复杂模型

现实：

Feature > Model

🚀 八、如果你愿意，我可以直接给你一个：
《AI量化工程师工业级项目模板（可直接开发）》

包含：

完整目录结构
模块接口设计
训练流水线代码架构
回测引擎架构
OMS设计
风险控制模块


甚至我可以给你：

🧱 C++ + Python 混合架构（非常适合你）

⚙️ Linux低延迟交易架构

🤖 AI模型训练流水线模板

🏭 Hedge Fund级系统架构图

只要你告诉我：

1️⃣ 你准备主力用 Python 还是 C++混合
2️⃣ 目标市场：股票 / 加密 / 期货 / 高频
3️⃣ 目标方向：自己交易赚钱 / 做量化工程师 / 做研究员

我可以给你一份 真正可开工的工业级项目蓝图。



### A股蓝图

下面是一份 面向“自己交易赚钱 + 股票市场”的工业级 AI量化项目蓝图。目标不是写demo，而是让你 从 Day-1 就在搭建可长期迭代、可实盘的系统。
我按真实私募/自营团队的研究→训练→回测→实盘链路设计，同时考虑你具备工程背景，可走 Python主导 + 可选C++加速 架构。

🧭 一、项目目标（明确范围）

市场：股票（US / A股二选一，接口不同但架构一致）
周期：日频 / 30min（先从中低频，减少噪声与成本）
策略类型：AI多因子选股 + 风险控制
系统能力：

✔ 自动下载数据
✔ 自动生成因子
✔ 自动训练模型（Walk-forward）
✔ 事件驱动回测
✔ 实盘下单（API）
✔ 风险控制与监控
✔ 模型与策略版本管理

🏗 二、总体系统架构（可直接照此建仓库）
quant-trading-system/
├── data/            # 数据采集/清洗/存储
├── features/        # 因子工程
├── models/          # ML训练与预测
├── backtest/        # 回测引擎
├── portfolio/       # 组合与仓位
├── execution/       # 交易接口/OMS
├── risk/            # 风控
├── research/        # 策略研究notebooks
├── configs/         # YAML配置
├── pipelines/       # 训练/回测流水线
├── utils/
└── main.py

🧱 三、技术选型（务实组合）
语言与框架

Python 3.11+（主）

可选 C++：撮合/回测核心、特征计算加速（后期）

数据与计算

pandas + polars（特征快）
DuckDB（本地分析数据库）
Parquet（统一存储格式）

机器学习
LightGBM（主力）
sklearn pipeline
optuna（自动调参）
mlflow（模型版本）


回测
自研事件驱动（建议）
或 vectorbt（快速起步）
实盘接口（股票）
US：IBKR / Alpaca
A股：掘金 / 米筐 / QMT（取决于券商）

🔁 四、核心数据流（你要实现的Pipeline）
[Data Ingest]
    ↓
[Data Clean + Align]
    ↓
[Feature DAG]
    ↓
[Labeling]
    ↓
[Walk-forward Train]
    ↓
[Signal]
    ↓
[Portfolio Construction]
    ↓
[Backtest / Live Execution]
    ↓
[Risk Engine + Monitoring]

🧮 五、因子工程（第一批就能用）
价格类

Momentum(5/20/60)

Rolling Mean / Z-score

Breakout(N日新高/低)

波动率

ATR

Rolling Std

Parkinson Vol

量价

OBV

Volume Spike

Turnover

横截面

行业中性化

市值分组

Rank IC

原则：少而稳，先20–40个高质量因子。

🤖 六、模型与训练（工业流程）
标签（示例）
y = future_5d_return

训练方式（必须）

Walk-forward

Purged K-Fold（避免信息泄露）

时间序列CV（禁止随机切分）

模型

LightGBM Regressor（回归收益）

Logistic（上涨概率）

输出
signal = rank(prediction)

📊 七、回测引擎（必须具备的机制）
事件驱动（bar/日）
滑点模型（bps）
手续费模型
涨跌停/停牌处理（A股）
成交量限制
延迟（T+1/T+0规则）


指标：

CAGR

Sharpe

Sortino

Max Drawdown

Turnover

IC / ICIR

💼 八、组合与仓位（赚钱关键）

基础组合器：

Top N Long
等权 / 波动率加权
行业中性（可选）
最大单票权重
最大行业暴露


风险缩放：

target_vol = 10%
position *= target_vol / realized_vol

🛒 九、执行与OMS（最小可用版）

模块：

OrderManager

PositionBook

FillHandler

BrokerAdapter

流程：

signal → target weights → orders → broker API → fills → positions


容错：

重试

断线恢复

幂等下单ID

🛡 十、风控（务必上线前完成）

单日最大亏损（如 -2% 停止交易）

最大回撤阈值（如 -15% 降杠杆）

单票最大仓位（如 5%）

流动性过滤（ADV阈值）

黑名单（财报/停牌）

🚀 十一、90天可执行里程碑
Day 1–14

数据下载 → Parquet

因子库v1（20个）

vectorbt快速回测

Day 15–45

Walk-forward训练

LightGBM信号

组合构建

成本建模

Day 46–75

自研事件驱动回测

风控模块

mlflow模型管理

Day 76–90

接券商API（模拟盘）

实盘日志与监控

小资金灰度上线

📁 十二、关键接口（建议先定义）
class Feature:
    def compute(self, df) -> pd.DataFrame: ...

class Model:
    def fit(self, X, y): ...
    def predict(self, X): ...

class Portfolio:
    def build(self, signals, constraints): ...

class Broker:
    def send_orders(self, orders): ...

⚠️ 十三、上线前检查清单（务必执行）

 所有回测含手续费/滑点

 Walk-forward稳定 > 3年窗口

 多市场/多时期压力测试（如2020/2022）

 空仓期也测试

 参数敏感性分析（避免过拟合）

📦 如果你愿意，我可以直接给你下一步的「可直接开干」材料：

1️⃣ 完整项目目录 + 每个模块的代码骨架（Python版）
2️⃣ AI多因子训练流水线模板（LightGBM + Walk-forward）
3️⃣ 最小可用事件驱动回测引擎源码框架
4️⃣ 股票实盘执行OMS最小实现（IBKR 或 A股接口二选一）
5️⃣ C++加速点位设计（适合你做性能优化）

直接告诉我两点，我马上给你第一版工程模板：

① 目标市场：美股 还是 A股

② 你打算 纯Python先跑通，还是 Python + C++混合从一开始设计