# 02 · Dynamic Programming, Monte Carlo and TD Learning

## 三种 target 来源

| 方法 | target 怎样得到 | 是否需要模型 | 是否 bootstrap |
|---|---|---:|---:|
| DP | 对转移模型精确求期望 | 是 | 是 |
| MC | 等回合结束得到完整 return | 否 | 否 |
| TD(0) | 一步奖励 + 下一状态当前估计 | 否 | 是 |

## Policy Iteration 与 Value Iteration

Policy Iteration 把评估与改进分开：充分评估当前策略，再做一次贪心改进。

Value Iteration 把二者压缩到每次最优备份中：

`Vₖ₊₁(s)=maxₐ E[R+γVₖ(S') | s,a]`

两者都是 Generalized Policy Iteration：价值估计和策略改进互相推动。

## Monte Carlo

`V(s) ← V(s) + α[Gₜ - V(s)]`

MC 不需要模型，因为大数定律让样本平均逐渐接近期望。但完整回报会受到整条后续轨迹影响，因此通常方差较大。

Exploring Starts 和 ε-greedy 都在解决充分探索：前者是假设，后者是可执行的行为策略。

## TD(0)

`δₜ = Rₜ₊₁ + γV(Sₜ₊₁) - V(Sₜ)`

`V(Sₜ) ← V(Sₜ) + αδₜ`

TD 不用等待回合结束。代价是 target 使用当前估计，因此带来 bias；收益是更低方差和在线更新能力。

## Sarsa 与 Q-learning

Sarsa：

`Q(S,A) ← Q(S,A) + α[R + γQ(S',A') - Q(S,A)]`

下一动作 `A'` 来自实际行为策略，因此是 on-policy。

Q-learning：

`Q(S,A) ← Q(S,A) + α[R + γmaxₐQ(S',a) - Q(S,A)]`

行为策略可以探索，但 target 假设下一步贪心，因此是 off-policy。

判断口诀：**看 target 中的下一动作来自谁。**

## 我的理解

MC 与 TD 的核心差别不是“有没有公式”，而是 target 对未知未来的处理方式：

- MC 用真实未来替代估计；
- TD 用估计替代尚未发生的未来；
- n-step 在真实样本与估计之间选择截断点。
