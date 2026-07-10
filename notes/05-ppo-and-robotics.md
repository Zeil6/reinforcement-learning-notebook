# 05 · PPO, GAE and Robotics Practice

## PPO 从哪里来

PPO 可以沿着课程主线拆解：

1. Critic 估计状态价值；
2. TD error 衡量结果相对预期的变化；
3. GAE 把多个 TD error 组合为 advantage；
4. Actor 根据 advantage 更新动作概率；
5. Clipping 限制新旧策略差异。

## GAE

`δₜ = rₜ + γV(sₜ₊₁) - V(sₜ)`

`Âₜ = Σₗ(γλ)ˡδₜ₊ₗ`

- `λ` 小：更接近一步 TD，方差低、偏差可能更明显；
- `λ` 大：看得更远，通常偏差降低、方差增加。

## PPO Clipped Objective

`rₜ(θ)=πθ(aₜ|sₜ)/πold(aₜ|sₜ)`

`Lclip = E[min(rₜÂₜ, clip(rₜ,1-ε,1+ε)Âₜ)]`

概率比率衡量新策略相对旧策略改变了多少。Clipping 不是保证策略永远不变，而是让单轮更新保持在更可信的范围。

## Isaac Lab 配置翻译

| 配置 | 理论对象 | 我会观察什么 |
|---|---|---|
| observations | 状态表示 S | 信息完整性、量纲、归一化 |
| actions / action_scale | 动作 A | 饱和、抖动、响应范围 |
| reward terms / weights | 奖励 R | 分量冲突、尺度、奖励投机 |
| gamma | 折扣因子 | 长时信用分配 |
| lambda | GAE 折中 | advantage 方差、critic 偏差 |
| learning_rate | 随机近似步长 | KL、loss 震荡、停滞 |
| clip_param | 策略更新范围 | approx KL、clip fraction |
| num_envs × rollout | 样本批量 | 相关性、吞吐、更新频率 |
| episode length / termination | 回合边界 | 真终止、时间截断、bootstrap |

## TensorBoard 诊断顺序

1. 先看任务指标：return、episode length、成功率和各 reward term；
2. 再看 critic：value loss、explained variance；
3. 再看策略变化：entropy、approx KL、clip fraction；
4. 最后回放策略，检查曲线无法暴露的动作抖动和奖励投机。

## 一个重要工程判断

总奖励上升但关键误差不下降时，我不会立即认为训练成功。可能原因包括：

- 奖励尺度掩盖了关键分量；
- 策略利用终止条件或重置机制；
- 代理指标与真实任务目标不一致；
- critic 学会预测现有奖励，却没有推动期望行为。

奖励曲线、分项曲线和可视化回放必须相互验证。
