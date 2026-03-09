# 姚念铭 | 数据分析 Portfolio

> 数据分析（商业分析 / 增长分析）｜广州、深圳｜2025.07 毕业｜可随时到岗

擅长 **指标口径校验、实验评估与经营诊断**，能基于 `SQL / Python` 完成 **用户分层、预算优化和治理优先级分析**。

[简历 PDF](./姚念铭的简历.pdf) | [GitHub](https://github.com/CLampard-Y) | [联系我](mailto:nianmingyao.math@outlook.com)

## 如果你只看 10 秒

- `增长分析 / 实验评估（离线策略模拟）`：基于 `64,000` 用户 Hillstrom RCT，将平均实验结论转成预算内 top-K 投放优先级；top `25%` 用户 `ROI proxy 2.08x`、预算 `-75%`、保留 `51.9%` 增量转化
- `经营诊断 / 治理优先级（描述性证据）`：按 `订单 / 商品 / 用户` 三层粒度固化指标口径；评价覆盖率 `99.33%`，延迟从轻微到严重时评分中位数 `4 -> 1`，并将 `611` 个活跃卖家收敛至 `58` 个重点治理对象
- `分析基础设施 / 稳定供数（主备演示验证）`：设计 Airflow 跨区主备数据管道，已完成 `HK -> JP` 自动接管演示，支持幂等入库、来源追溯与 parquet 快照导出

注：为避免过度表述，项目 1 的收益数字来自 **离线策略模拟**，项目 2 主要提供 **描述性经营诊断证据**，项目 3 当前证明的是 **主备切换演示与运行验证**。

## 快速导航

- `HR / 招聘经理`：先看 [项目速览](#project-overview) + [核心能力](#skills) + [联系方式](#contact)
- `业务面试官`：重点看 [项目 1](#project-1) + [项目 2](#project-2)
- `技术面试官`：重点看 [核心能力](#skills) + [项目 1](#project-1) + [项目 3](#project-3)

<a id="skills"></a>

## 核心能力

- `SQL / Python`：PostgreSQL、CTE、JOIN、窗口函数、指标建模；pandas、numpy、scikit-learn、xgboost、SQLAlchemy
- `分析能力`：指标口径校验、实验评估、用户分层、增长分析、履约/留存分析、经营诊断、卖家治理
- `数据与工程`：Excel、ELT、OBT、DQ Gates、Airflow、Docker、Git、JupyterLab、运行检查、数据导出
- `项目映射`：项目 1 聚焦实验评估与预算优化；项目 2 聚焦经营诊断与治理优先级；项目 3 聚焦分析基础设施与稳定供数

<a id="project-overview"></a>

## 项目速览

### 1) 因果增量营销优化策略（Hillstrom RCT）

- `业务问题`：在“全量触达 vs 预算内定向触达”之间，确定预算该优先给谁
- `我的动作`：基于 `64,000` 用户 RCT，搭建 **实验评估 -> 增量排序 -> 名单输出 -> 策略执行** 链路
- `结果速览`：top `25%` 用户离线策略模拟下 `ROI proxy 2.08x`、预算 `-75%`、保留 `51.9%` 增量转化
- `主入口`：[Case Study](https://github.com/CLampard-Y/causal-uplift-marketing/blob/main/docs/case_study_one_pager.md) | [Repo](https://github.com/CLampard-Y/causal-uplift-marketing) | [README](https://github.com/CLampard-Y/causal-uplift-marketing/blob/main/README.md)

### 2) 电商增长分析与卖家治理项目（Olist）

- `业务问题`：如果不先守住订单 / 商品 / 用户三层粒度，履约、复购和卖家治理结论都可能失真
- `我的动作`：搭建 `CSV -> Postgres -> SQL models -> DQ gates -> notebooks` 的本地 ELT 分析链路，并将动作拆成 **首单品类筛选** 与 **卖家治理优先级**
- `结果速览`：评价覆盖率 `99.33%`；轻微延迟到严重延迟时评分中位数 `4 -> 1`；`611 -> 58` 卖家治理优先级
- `主入口`：[Execution Report](https://github.com/CLampard-Y/ecommerce-analytics-pipeline/blob/main/docs/execution_report.md) | [Repo](https://github.com/CLampard-Y/ecommerce-analytics-pipeline) | [README](https://github.com/CLampard-Y/ecommerce-analytics-pipeline/blob/main/README.md)

### 3) 分析基础设施与稳定供数（Airflow 主备切换）

- `业务问题`：区域节点故障时，行情数据还能否不断供、可追溯、可导出
- `我的动作`：搭建 **US 控制平面 + HK 主抓取 + JP 备援** 的 Airflow 编排链路，并用 `source_region` + upsert 做来源追踪与幂等入库
- `结果速览`：已完成 `HK -> JP` 自动接管演示，支持主备切换后的审计排查与 parquet 快照导出
- `主入口`：[Deployment Guide](https://github.com/CLampard-Y/resilient-market-data-pipeline/blob/main/DEPLOYMENT_GUIDE.md) | [Repo](https://github.com/CLampard-Y/resilient-market-data-pipeline) | [README](https://github.com/CLampard-Y/resilient-market-data-pipeline/blob/main/README.md)

<a id="project-1"></a>

## 项目 1：因果增量营销优化策略（Hillstrom RCT）

### 项目定位

围绕“**全量触达 vs 预算内定向触达**”，把平均 A/B 结论进一步翻译成 **用户级投放优先级**，回答预算该优先给谁。

### 核心动作

- 基于 `64,000` 用户 Hillstrom RCT，搭建 **实验评估 -> 增量排序 -> 名单输出 -> 策略执行** 的完整链路
- 审计实验分组与特征口径，排除后置变量，并做可比性与稳健性检查，降低将随机波动误判为投放机会的风险
- 对比多种 uplift / CATE 排序方案，选择最优模型，并用 SQL 将结果转化为预算内 top-K 名单与用户分层
- 将模型输出落到 `top 25%` 用户 / `Persuadables only` 的离线策略模拟，而不是停在模型分数比较

### 已验证结果

- `数据规模`：`64,000` 用户公开 RCT
- `低转化场景`：整体转化率 `0.9031%`
- `因果基线`：Naive ATE `+0.4955%`；PSM ATE `0.502%`，`95% CI [0.324%, 0.690%]`
- `排序结果`：`X-Learner` 为当前最优 uplift learner，默认策略落在 `Persuadables only` / top `25%` 用户
- `策略输出`：离线策略模拟下 **ROI proxy `2.08x`**、**预算 `-75%`**、**保留 `51.9%` 增量转化**

### 核心竞争力

- 我能把 **平均实验结论** 往前推进到 **用户级投放优先级**
- 我不会只报模型分数，而会主动回答 **这个结果如何影响预算配置和业务动作**
- 我能在分析叙事里同时兼顾 **方法可信度** 和 **商业可读性**

### 查看这个项目

- [Case Study](https://github.com/CLampard-Y/causal-uplift-marketing/blob/main/docs/case_study_one_pager.md)
- [Repo](https://github.com/CLampard-Y/causal-uplift-marketing)
- [README](https://github.com/CLampard-Y/causal-uplift-marketing/blob/main/README.md)

### 结果边界

- 以上 `ROI proxy 2.08x`、`预算 -75%`、`保留 51.9% 增量转化` 均来自 **离线策略模拟**，用于比较策略优先级，不等同于真实线上财务结果

<a id="project-2"></a>

## 项目 2：电商增长分析与卖家治理项目（Olist）

### 项目定位

按 **订单 / 商品 / 用户** 三层粒度固化指标口径，先确认什么能信，再判断履约、复购和卖家治理该怎么做。

### 核心动作

- 搭建 `CSV -> Postgres -> SQL models -> DQ gates -> notebooks` 的本地 ELT 分析链路
- 按 `订单 / 商品 / 用户` 三层粒度固化指标口径，降低连接扇出与分母漂移导致的误判风险
- 识别履约体验断崖：围绕延迟交付、评价覆盖和评分变化，确认体验恶化的关键边界
- 在确认平台低复购后，将动作拆成 **首单品类筛选** 与 **卖家治理优先级** 两条分支，而不是硬讲复购增长故事

### 已验证结果

- `指标可信度`：评价覆盖率 `99.33%`
- `履约断崖`：延迟从 `Late_Small` 进入 `Late_Severe` 时，评分中位数由 `4.0 -> 1.0`
- `差评风险`：延迟交付是差评核心风险因子之一（OR `2.2048`，描述性基线）
- `低复购现实`：eligible `90d` 复购率 `1.30%`
- `治理输出`：将 `611` 个活跃卖家收敛至 `58` 个重点治理对象

### 核心竞争力

- 我会先做 **粒度 / 分母 control**，再进入业务解释，而不是直接从图表编故事
- 我能把经营问题拆成 **measurement problem** 和 **decision problem** 两层
- 我能把 SQL 建模、DQ 门禁和 notebook 诊断连成一条真正可复查的分析链路

### 查看这个项目

- [Execution Report](https://github.com/CLampard-Y/ecommerce-analytics-pipeline/blob/main/docs/execution_report.md)
- [Repo](https://github.com/CLampard-Y/ecommerce-analytics-pipeline)
- [README](https://github.com/CLampard-Y/ecommerce-analytics-pipeline/blob/main/README.md)

### 结果边界

- `OR 2.2048` 与 `90d` 复购率结论分别属于 **描述性经营诊断** 与 **eligible 分母口径** 下的结果，不应被讲成因果识别或真实 ROI 归因

<a id="project-3"></a>

## 项目 3：分析基础设施与稳定供数（Airflow 主备切换）

### 项目定位

围绕 **主节点失败自动切换 + 幂等入库 + 审计排查**，设计一条跨区主备数据爬虫管道，为下游监控、图表和分析提供稳定输入。

### 核心动作

- 在 US 节点集中部署 `Airflow + Postgres` 作为控制平面与存储中心，由 HK 节点负责常规抓取、JP 节点负责故障接管
- 通过 `SSHOperator` 调度远端 crawler 容器，主路径失败时用 `TriggerRule.ALL_FAILED` 自动放开 JP 备援路径
- 用 `UNIQUE(symbol, interval, open_time)` + upsert 保证重跑与主备切换不会制造重复行
- 通过 `source_region`、Dashboard 和 Exporter 保留来源标签、运行轨迹与近 `24` 小时 parquet 快照，支持审计与下游消费

### 已验证结果

- `调度频率`：Airflow 主 DAG 按小时运行
- `抓取范围`：默认抓取 `4` 个 symbol、各自近 `24` 根小时 K 线
- `容灾演示`：已验证 `HK-Primary` 正常写回，以及 `HK` 失败后 `JP-Backup` 自动接管
- `幂等入库`：`UNIQUE(symbol, interval, open_time)` + upsert 保证重跑不产生重复行
- `可追溯输出`：数据表和日志保留 `source_region`，并已生成 parquet 快照示例

### 核心竞争力

- 我知道分析岗位真正依赖的不只是 SQL/Python，而是 **稳定供数 + 可追溯数据来源**
- 我能把故障切换设计成 **可运行、可验证、可审计** 的链路，而不是只画 HA 架构图
- 我能把这个项目放在 **分析基础设施** 语境下讲清楚，而不是把它包装成脱离业务的数据工程炫技

### 查看这个项目

- [Deployment Guide](https://github.com/CLampard-Y/resilient-market-data-pipeline/blob/main/DEPLOYMENT_GUIDE.md)
- [Validation Snapshots](https://github.com/CLampard-Y/resilient-market-data-pipeline/blob/main/docs/validation/README.md)
- [Repo](https://github.com/CLampard-Y/resilient-market-data-pipeline)
- [README](https://github.com/CLampard-Y/resilient-market-data-pipeline/blob/main/README.md)

### 结果边界

- 当前证据支持的是 **主备切换演示与运行验证**，不是完整生产级 HA / SRE 体系；它更适合被理解为 **分析基础设施与稳定供数能力** 的作品证明

<a id="contact"></a>

## 联系方式

- `简历 PDF`：[姚念铭的简历.pdf](./姚念铭的简历.pdf)
- `项目主页`：[data-analysis-portfolio](https://github.com/CLampard-Y/data-analysis-portfolio)
- `GitHub`：[CLampard-Y](https://github.com/CLampard-Y)
- `Email`：[nianmingyao.math@outlook.com](mailto:nianmingyao.math@outlook.com)
