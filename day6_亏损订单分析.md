
# 📊 Day6：亏损订单分析

在前几天的探索中，我们发现了一些利润为负的州，以及总体上利润较低的子类。今天我们进一步挖掘这些亏损订单，找出其中“最亏”的 Top10，并分析它们的子类构成，辅助业务优化。

---

## ✅ Step 1：筛选出亏损州的数据

我们刚才得到了亏损州列表（`loss_states_sorted`），现在从原始数据 `df` 中，把这些州的数据筛选出来：

```python
# 取出亏损州的原始交易数据
loss_state_names = loss_states_sorted.index.tolist()  # 获取州名称列表
loss_state_df = df[df['State'].isin(loss_state_names)]  # 用 isin 进行筛选
```

---

## ✅ Step 2：绘制箱线图，查看各州利润分布

为了观察各州的利润分布是否存在极端值，我们绘制箱线图：

```python
plt.figure(figsize=(12, 6))
sns.boxplot(data=loss_state_df, x='Profit', y='State', orient='h')
plt.title('亏损州的利润分布（箱线图）')
plt.xlabel('Profit')
plt.ylabel('State')
plt.tight_layout()
plt.show()
```

我们可以从图中观察到是否存在 **极端亏损订单** —— 这些可能是影响整体利润的关键点。

---

## ✅ Step 3：找出利润最差的 Top10 订单

接下来我们将所有订单按利润升序排列，并取出最亏的前10个订单：

```python
worst_orders = df.sort_values(by='Profit').head(10)
print(worst_orders)
```

---

## ✅ Step 4：分析这些订单涉及的子类

我们统计这 10 个订单中，涉及的商品子类的总亏损金额：

```python
worst_subcat_summary = (
    worst_orders.groupby('Sub-Category')['Profit'].sum()
    .sort_values()
)

# 绘图展示
worst_subcat_summary.plot(kind='barh', color='tomato')
plt.title('Top10最亏订单中，各子类亏损汇总')
plt.xlabel('利润')
plt.ylabel('子类')
plt.tight_layout()
plt.show()
```

---

## 📝 总结

我们今天完成了以下内容：

- 从亏损州中筛选出所有交易记录；
- 使用箱线图查看利润的分布情况；
- 找出了利润最差的 Top10 订单；
- 分析了这些订单主要集中在哪些子类中。

下一步我们将尝试通过构建模型，对这些亏损进行预测！

