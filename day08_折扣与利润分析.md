
# Day 8 折扣与利润分析：负相关关系的可视化与验证

今天我们探索了在亏损州（`loss_state_df`）中，商品的“折扣”与“利润”之间是否存在某种关系。
通过可视化和统计方法，我们验证了两者之间确实存在**负相关**。

---

## 一、散点图：折扣与利润的关系

我们提取了折扣和利润的两列数据，并绘制了基础散点图：

```python
discount_profit_df = loss_state_df[['Discount', 'Profit']]
plt.figure(figsize=(8, 5))
plt.scatter(discount_profit_df['Discount'], discount_profit_df['Profit'], alpha=0.5)
plt.title('折扣与利润的关系（散点图）')
plt.xlabel('折扣')
plt.ylabel('利润')
plt.grid(True)
plt.show()
```

随后添加趋势线（回归线）以观察走势：

```python
# 计算拟合
z = np.polyfit(discount_profit_df['Discount'], discount_profit_df['Profit'], 1)
p = np.poly1d(z)

# 叠加趋势线
plt.figure(figsize=(8, 5))
plt.scatter(discount_profit_df['Discount'], discount_profit_df['Profit'], alpha=0.5)
plt.plot(discount_profit_df['Discount'], p(discount_profit_df['Discount']), color='red', linewidth=2)
plt.title('折扣与利润的关系（含趋势线）')
plt.xlabel('折扣')
plt.ylabel('利润')
plt.grid(True)
plt.show()
```

---

## 二、相关系数计算与热力图验证

我们使用 `.corr()` 方法计算相关系数：

```python
correlation = discount_profit_df.corr()
print(correlation)
```

输出结果如下：

|            | Discount | Profit  |
|------------|----------|---------|
| Discount   | 1.000000 | -0.2259 |
| Profit     | -0.2259  | 1.00000 |

我们绘制了热力图进一步验证：

```python
sns.heatmap(correlation, annot=True, cmap='RdBu', center=0, fmt=".2f")
plt.title("折扣与利润的相关系数热力图")
plt.show()
```

---

## ✅ 结论

- 在亏损州订单中，**折扣与利润存在负相关关系**；
- 折扣越高，利润越有可能下降；
- 可通过设定合理折扣策略来优化利润表现。
