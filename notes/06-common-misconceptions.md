# 06 · Common Misconceptions

| 容易混淆 | 最简区分 |
|---|---|
| reward vs return | 一步反馈 vs 未来奖励折扣和 |
| trajectory vs episode | 状态动作序列 vs 有开始和终止的一次试验 |
| V vs Q | 按策略平均动作 vs 先固定具体动作 |
| max vs argmax | 最大数值 vs 实现最大值的动作 |
| `v=f(v)` vs `vₖ₊₁=f(vₖ)` | 固定点条件 vs 求解迭代 |
| prediction vs control | 评价策略 vs 同时改进策略 |
| model-based vs model-free | 使用环境模型 vs 直接从样本学习 |
| MC vs TD | 完整回报 vs 一步奖励加估计 |
| on-policy vs off-policy | 行为策略与目标策略相同 vs 不同 |
| sample vs expectation | 一次随机结果 vs 所有结果的加权平均 |
| value vs advantage | 绝对长期表现 vs 相对平均表现 |
| actor vs critic | 决定动作 vs 估计价值并提供学习信号 |
| learning rate α vs discount γ | 参数每次改多少 vs 未来奖励算多重 |
| env step vs gradient update | 一次环境交互不等于一次网络更新 |

## 三个特别容易影响代码理解的点

### 1. `S~η, A~π` 不等于两个求和符号

`~` 表示实际采样；求和表达式表示精确期望。样本均值在样本足够多时近似期望，但单个样本不是完整期望。

### 2. Critic 不产生 reward

环境产生 reward。Critic 学习价值估计，把一步 reward 与未来回报连接起来。

### 3. Off-policy 不等于“用了 replay buffer”

定义看的是行为策略和目标策略是否不同。Replay buffer 常与 off-policy 配合，但不是定义本身。
