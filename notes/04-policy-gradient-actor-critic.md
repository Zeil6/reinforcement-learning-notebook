# 04 · Policy Gradient and Actor–Critic

## 为什么直接优化策略

连续动作下无法像离散 Q-learning 那样枚举全部动作取 `max`。策略梯度将策略参数化为 `πθ(a|s)`，直接最大化期望回报。

`∇θJ = E[∇θ log πθ(A|S) Qπ(S,A)]`

直觉是：

- 一个动作的结果好于预期，就提高其概率；
- 差于预期，就降低其概率；
- 改变幅度由回报或 advantage 决定。

## 为什么使用 log π

恒等式：

`∇θπθ(a|s) = πθ(a|s)∇θlogπθ(a|s)`

它把对概率分布的梯度转换为可以由采样估计的 score function。

## REINFORCE 与 baseline

`θ ← θ + αGₜ∇θlogπθ(Aₜ|Sₜ)`

完整回报方差大。减去只依赖状态的 baseline 不改变期望梯度：

`θ ← θ + α[Gₜ-b(Sₜ)]∇θlogπθ(Aₜ|Sₜ)`

若 `b(s)=Vπ(s)`，括号中的量就在估计动作相对平均表现。

## Advantage

`Aπ(s,a)=Qπ(s,a)-Vπ(s)`

Advantage 比绝对 Q 更适合指导策略：它回答“这个动作是否比当前策略在该状态下的平均选择更好”。

## Actor–Critic

- Actor：输出动作分布或确定性动作；
- Critic：估计 V 或 Q，提供低方差学习信号。

当 `V=Vπ` 时：

`E[δₜ | Sₜ=s,Aₜ=a] = Aπ(s,a)`

因此 TD error 可以作为 advantage 的单样本估计。单个 `δ` 不是精确 advantage，而是带噪声的估计。

## Off-policy Actor–Critic

行为策略 `μ` 与目标策略 `π` 不同时，可使用重要性比率：

`ρₜ = π(Aₜ|Sₜ) / μ(Aₜ|Sₜ)`

比率过大会放大方差，这也是 clipping、trust region 等稳定化思路出现的重要背景。
