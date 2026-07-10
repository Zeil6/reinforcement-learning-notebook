# Roadmap

## 近期：把理解变成可复现实验

- [ ] GridWorld：对比 Policy Iteration 与 Value Iteration 的收敛过程
- [ ] Cliff Walking：对比 Sarsa 与 Q-learning 的风险偏好
- [ ] Random Walk：对比 MC、TD(0) 与 n-step 的 RMSE
- [ ] CartPole：实现 REINFORCE、baseline 与 Actor–Critic 的方差对比
- [ ] PPO：记录 GAE λ、clip range 与 KL / return 的关系

## 中期：连接机器人任务

- [ ] 整理 Isaac Lab 训练配置到 MDP 元素的映射模板
- [ ] 对 xMimic 跟踪奖励做单变量消融实验
- [ ] 记录 checkpoint 恢复、评估与 TensorBoard 对齐方法
- [ ] 对连续动作任务比较 PPO、DDPG/TD3 的适用边界

## 输出标准

每个实验都至少包含：

1. 要验证的问题；
2. 理论预期；
3. 控制变量；
4. 指标与曲线；
5. 失败结果与解释；
6. 对下一次实验的影响。

我希望这个仓库的每次更新都回答一个问题，而不是只增加代码量。
