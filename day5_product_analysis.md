
# 📊 Day 5：商品子类销售与利润分析

本日任务目标：使用 Pandas 和 Matplotlib 对商品子类的销售金额与利润进行可视化分析，并筛选出亏损的商品子类。

---

## ✅ 步骤 1：按商品子类分组，汇总销售额和利润

```python
subcat_profit = df.groupby('Sub-Category')[['Sales', 'Profit']].sum()
```

---

## ✅ 步骤 2：绘制销售额与利润的对比柱状图

```python
subcat_profit.plot(kind='bar', figsize=(14, 6), color=['lightgreen', 'skyblue'])
plt.title('商品子类的销售额与利润')
plt.xlabel('商品子类')
plt.ylabel('金额')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

🔍 **解读：**
- 使用 `.plot(kind='bar')` 快速画出对比柱状图。
- `color` 参数自定义颜色，`rotation=45` 旋转 x 轴标签方便阅读。

---

## ✅ 步骤 3：筛选利润为负的子类

```python
loss_subcat = subcat_profit[subcat_profit['Profit'] < 0]
```

🔍 **说明：**
- 这一步利用了 Pandas 的布尔索引功能，只保留利润为负的行。

---

## ✅ 步骤 4：绘制亏损商品子类的横向条形图

```python
loss_subcat['Profit'].sort_values().plot(kind='barh', color='salmon')
plt.title('利润为负的商品子类')
plt.xlabel('利润')
plt.ylabel('商品子类')
plt.tight_layout()
plt.show()
```

🧾 **解读：**
- 使用 `barh` 横向柱状图展示。
- `sort_values()` 让亏损从大到小更直观。
- 色彩使用淡红色（salmon）以强调亏损性质。

---

## 🎯 总结

- 使用 `groupby + sum()` 可以快速做出多列聚合。
- `DataFrame.plot()` 是快速原型绘图的利器。
- 用布尔索引可以轻松过滤出感兴趣的数据子集。

---

