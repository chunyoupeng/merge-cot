# 新的论文模版放进去

# 添加例子进去

# 在训练集和测试集上面应该说明为什么使用8:1:1

# 量化数据

- [ ] 量化第 6.1 节计算开销（训练/推理成本、时延、调用次数等），给出可复现实验数字。
  - 训练：记录教师模型生成成本（调用次数、平均/总 token、总费用或 GPU 时长）、SFT 微调开销（epoch、batch、硬件、时长）。
  - 推理：单样本平均时延、平均 token、并发设置、稳定性（超时/失败率）。
  - 以统一单位呈现成本（如 USD/万样本、GPU-hour/epoch）并提供估算脚本或表格。

  针对数据量是10万条，调用次数10万次，平均token 2000左右，中token 2,000*100,000=200,000,000 token
总gpu时长在Nvidia 5090 * 2 时长是38h

微调开销是8个h

- 基础模型：Qwen2.5 7B。
- 优化器：AdamW，学习率 5 × 10⁻⁵。
- Batch size：32。
- epoch 2
- 每种语言的训练耗时：8–12 小时。
- 推理阶段采用自洽多数投票（30 次采样，温度 0.7）。
- 实验硬件：Dell Precision 7920 Tower，双 Intel Xeon Gold 5218 CPU、两块 NVIDIA GeForce RTX 3090 GPU、64 GB RAM。


## 训练数据情况

我们一共的数据有这些，下面是每一种的分布
我们采用的是MergeCoT. mergebert一样的数据，只不过首先于文本的长度，我们去掉了过长（长与2048token和过短的数据小于5个token，数据太短的大多是一些标点符号之类的，我们认为对于我们的任务是没有正收益的）


训练话费的token 数量是（70150 + 8768）*2048 = 161,624,064 token
平均每一条数据输入输出总共是1000token，那么跑整个数据集一共的token花销是 8772 * 2048 约等于 17,965,056 token（推理部分）

total records: 87690

Per dataset & split:
  - csharp-cot       test         1188 (  1.35%)
  - csharp-cot       train        9498 ( 10.83%)
  - csharp-cot       val          1187 (  1.35%)
  - java-cot         test         3982 (  4.54%)
  - java-cot         train       31851 ( 36.32%)
  - java-cot         val          3981 (  4.54%)
  - javascript-cot   test         2691 (  3.07%)
  - javascript-cot   train       21520 ( 24.54%)
  - javascript-cot   val          2690 (  3.07%)
  - typescript-cot   test          911 (  1.04%)
  - typescript-cot   train        7281 (  8.30%)
  - typescript-cot   val           910 (  1.04%)

Per dataset:
  - csharp-cot              11873 ( 13.54%)
  - java-cot                39814 ( 45.40%)
  - javascript-cot          26901 ( 30.68%)
  - typescript-cot           9102 ( 10.38%)

Per split:
  - test                     8772 ( 10.00%)
  - train                   70150 ( 80.00%)
  - val                      8768 ( 10.00%)

