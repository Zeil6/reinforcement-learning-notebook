# 20 Core Reinforcement Learning Questions

这些问题用于检查自己是否真正建立了知识连接，而不只是记住名词。

1. 为什么 `Vπ(s)` 是 `Qπ(s,a)` 对动作分布的平均，而不是与每个 Q 都相等？
2. Bellman 方程为什么能把无限未来压缩成一步递推？马尔可夫性在哪里被使用？
3. `v=f(v)` 与 `vₖ₊₁=f(vₖ)` 分别在说什么？`γ<1` 为什么重要？
4. Policy Iteration 与 Value Iteration 的“评估—改进”粒度有什么差别？
5. MC 为什么不需要环境模型？大数定律扮演什么角色？
6. Exploring Starts 与 ε-greedy 分别怎样保证探索？
7. Robbins–Monro 的两条步长条件直觉上各防止什么问题？
8. MC target 与 TD target 的信息来源、偏差和方差有何不同？
9. 只看更新式，怎样判断算法是 on-policy 还是 off-policy？
10. Sarsa 与 Q-learning 在风险任务中为什么可能学习出不同策略？
11. 函数逼近为什么能泛化？为什么一个样本会影响许多状态？
12. DQN 的 replay buffer 与 target network 分别解决什么不稳定？
13. `S~η, A~π` 与 `ΣηΣπ` 是什么关系？
14. 策略梯度为什么使用 `∇logπ`？
15. 为什么减去 state-only baseline 不改变期望梯度，却能降低方差？
16. `Aπ(s,a)` 与 `Qπ(s,a)` 的含义差别是什么？
17. 当 V 精确时，TD error 的条件期望为什么等于 Advantage？
18. Off-policy Actor–Critic 为什么需要重要性采样？比率很大有什么风险？
19. DPG 为什么不使用 `∇logπ`？它怎样从 critic 获得动作改进方向？
20. PPO 的 GAE 和 clipping 分别继承并改进了课程中的什么问题？

## 自我评价标准

- **初步理解**：能口头解释 12 题；
- **形成体系**：能解释 16 题，并把公式串到前后章节；
- **可迁移**：能回答 18 题以上，并在 PPO / DQN 代码中指出相应实现。
