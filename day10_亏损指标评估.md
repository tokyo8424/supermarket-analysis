# Day 10 亏损指标评估：平均每单与每件商品的亏损分析

今天我们进行了对亏损订单的深入指标评估，目标是理解亏损集中在哪些层面：单个订单，还是单件商品。主要分析包括：

---

## 一、计算平均每单亏损金额

```python
avg_loss_per_order = loss_state_df['Profit'].mean()
print(f"每单平均亏损金额：{{avg_loss_per_order:.2f}}")
```

📌 **结果**：约为 **-25.33**

---

## 二、计算平均每件商品的亏损金额

```python
total_profit = loss_state_df['Profit'].sum()
total_quantity = loss_state_df['Quantity'].sum()
avg_loss_per_item = total_profit / total_quantity
print(f"每件商品平均亏损金额：{{avg_loss_per_item:.2f}}")
```

📌 **结果**：约为 **-6.74**

---

## 三、可视化比较两项指标

我们通过横向条形图比较这两个指标的差异：

```python
import matplotlib.pyplot as plt

plt.barh(['每单平均亏损金额', '每件商品平均亏损金额'], [avg_loss_per_order, avg_loss_per_item], color='tomato')
plt.title('每单 vs 每件商品的平均亏损对比')
plt.xlabel('亏损金额')
plt.grid(True)
plt.show()
```

📈 图表清晰显示：

- 每单亏损金额远高于每件商品亏损金额。

---

## 四、分析结论

- **单个订单的亏损额远大于单件商品的平均亏损**，说明亏损并非主要由商品定价导致。
- 高额订单、整单优惠、组合促销、配送策略等因素可能是亏损的关键来源。
- 建议未来分析中重点关注「订单层级」的促销和优惠机制。

---

下一步我们将进入 Day11，尝试识别特定高风险客户、商品或订单策略模式。