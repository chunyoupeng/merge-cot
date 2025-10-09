# 表 1–4 差值汇总（±x%）

说明：以下均以 `Δ = MergeCoT − 基线` 计算，单位为百分比点（pp）。

## 表 1：Java 整体效果（Precision/Accuracy）

| 基线模型    | Precision | Accuracy | ΔPrecision | ΔAccuracy |
|-------------|-----------|----------|------------|-----------|
| diff3       | 85.5      | 2.2      | -13.1      | 70.1      |
| JDIME       | 26.3      | 21.6     | 46.1       | 50.7      |
| MergeBERT   | 63.9      | 63.2     | 8.5        | 9.1       |
| ChatMerge   | 63.5      | 65.0     | 8.9        | 7.3       |
| MergeGen    | 69.2      | 67.7     | 3.2        | 4.6       |
| MergeCoT    | 72.4      | 72.3     | —          | —         |

注：MergeCoT 基准（72.4 / 72.3）。

## 表 2：多语言结果（Precision/Accuracy）

### Java

| 模型       | Precision | Accuracy | ΔPrecision | ΔAccuracy |
|------------|-----------|----------|------------|-----------|
| MergeBERT  | 63.9      | 63.2     | 8.5        | 9.1       |
| MergeGen   | 69.2      | 67.7     | 3.2        | 4.6       |
| MergeCoT   | 72.4      | 72.3     | —          | —         |

### C#

| 模型       | Precision | Accuracy | ΔPrecision | ΔAccuracy |
|------------|-----------|----------|------------|-----------|
| MergeBERT  | 68.7      | 67.3     | 10.3       | 7.8       |
| MergeGen   | 75.4      | 73.8     | 3.6        | 1.3       |
| MergeCoT   | 79.0      | 75.1     | —          | —         |

### JavaScript

| 模型        | Precision | Accuracy | ΔPrecision | ΔAccuracy |
|-------------|-----------|----------|------------|-----------|
| MergeBERT   | 66.9      | 65.6     | 5.3        | 4.9       |
| jsFSTMerge  | 15.8      | 3.6      | 56.4       | 66.9      |
| MergeGen    | 70.9      | 68.3     | 1.3        | 2.2       |
| MergeCoT    | 72.2      | 70.5     | —          | —         |

### TypeScript

| 模型       | Precision | Accuracy | ΔPrecision | ΔAccuracy |
|------------|-----------|----------|------------|-----------|
| MergeBERT  | 69.1      | 68.2     | 7.0        | 6.3       |
| DeepMerge  | 64.5      | 42.7     | 11.6       | 31.8      |
| MergeGen   | n/a       | n/a      | n/a        | n/a       |
| MergeCoT   | 76.1      | 74.5     | —          | —         |

## 表 3：ES 有效性消融（Java）

| 模型            | Precision | Accuracy | ΔPrecision | ΔAccuracy |
|-----------------|-----------|----------|------------|-----------|
| MergeCoT w/o ES | 70.7      | 70.4     | 1.7        | 1.9       |
| MergeCoT        | 72.4      | 72.3     | —          | —         |

注：此表中 Δ 仅为“MergeCoT − w/o ES”。

## 表 4：未知语言泛化（仅用 Java 训练）

| 语言        | 模型             | Precision | Accuracy | ΔPrecision | ΔAccuracy |
|-------------|------------------|-----------|----------|------------|-----------|
| JavaScript  | Direct Generation| 66.2      | 65.3     | 2.5        | 2.6       |
| JavaScript  | MergeCoT         | 68.7      | 67.9     | —          | —         |
| TypeScript  | Direct Generation| 64.5      | 60.8     | 2.0        | 1.3       |
| TypeScript  | MergeCoT         | 66.5      | 62.1     | —          | —         |

