# 03 · Function Approximation and DQN

## 为什么需要函数逼近

表格方法默认每个状态有独立存储位置。高维或连续状态下，这既不可存储，也无法从已见状态泛化到相似状态。

函数逼近把价值写成：

`V̂(s,w)` 或 `Q̂(s,a,w)`

共享参数带来泛化，也带来耦合：更新一个样本会改变许多状态的输出。

## 半梯度 TD

`w ← w + α[Target - V̂(S,w)]∇wV̂(S,w)`

TD target 中也包含估计值，但半梯度方法在当前更新中把 target 当作常数。这个处理简单有效，却不等同于对完整目标函数做真正梯度下降。

## DQN 的 target

`y = r + γ(1-done) maxₐ Q(s',a;θ⁻)`

`L(θ)=E[(y-Q(s,a;θ))²]`

## 三个稳定性机制

### Replay Buffer

随机抽取旧经验，打破相邻时间步的相关性，并提高数据复用率。

### Target Network

用较慢更新的 `θ⁻` 构造 target，减少预测网络和目标同时快速移动的问题。

### ε-Greedy

价值网络负责利用，行为策略负责探索。二者分工也使 DQN 成为典型 off-policy 方法。

## Deadly Triad

以下三项同时出现时可能导致发散：

- function approximation；
- bootstrapping；
- off-policy learning。

DQN 的设计缓解了风险，但不能把“训练没有报错”当作“学习过程稳定”。我会同时观察回报、Q 值尺度、TD error、梯度范数和回放策略。
