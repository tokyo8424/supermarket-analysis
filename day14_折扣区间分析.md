
# 📊 Day14：折扣策略与利润分析

## 🗂️ 分析目标

分析订单数据中不同折扣区间对平均利润的影响，帮助制定更合理的折扣策略，提升整体盈利能力。

---

## 🔧 操作步骤

### 1️⃣ 创建折扣区间

将 `Discount`（折扣）字段划分为若干区间：

```python
df['Discount_Bin'] = pd.cut(df['Discount'],
                            bins=[0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 1.0],
                            include_lowest=True)
```

### 2️⃣ 计算各折扣区间的平均利润

```python
discount_profit = df.groupby('Discount_Bin')['Profit'].mean().sort_index()
print(discount_profit)
```

输出结果如下：

```
Discount_Bin
(-0.001, 0.1]     67.46
(0.1, 0.2]        24.74
(0.2, 0.3]       -45.68
(0.3, 0.4]      -109.22
(0.4, 0.5]      -298.70
(0.5, 0.6]       -43.08
(0.6, 1.0]       -98.35
```

### 3️⃣ 可视化结果

```python
discount_profit.plot(kind='bar', color='salmon')
plt.title("不同折扣区间的平均利润")
plt.xlabel("折扣区间")
plt.ylabel("平均利润")
plt.grid(True, axis='y', linestyle='--', alpha=0.5)
plt.tight_layout()
plt.show()
```

📈 效果如下：

> 折扣高于 0.2 时平均利润普遍转负，0.4–0.5 折扣区间亏损最严重。

---

## 📌 分析结论

- 折扣控制在 **10%–20%** 内较为合理，利润仍为正值。
- 超过 30% 折扣将极大压缩利润，甚至导致严重亏损。
- 建议对高折扣订单进行进一步监控或重新评估定价策略。

---

## ✅ 今日总结

- 掌握 `pd.cut()` 连续数值离散化方法；
- 运用分组与平均值分析利润表现；
- 可视化支持洞察表达，为业务策略提供量化依据。
