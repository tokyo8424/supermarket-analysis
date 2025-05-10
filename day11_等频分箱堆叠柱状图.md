
# Day 11 等频分箱堆叠柱状图：销售额与商品类别的关系分析

今天我们聚焦于探索不同销售额区间中，不同商品类别的订单数量分布情况。为了更公平地将数据按销售额进行分组，我们使用 `qcut` 方法进行等频分箱（即每组订单数量相近），并在每个销售额区间中统计不同商品类别的订单数量，绘制堆叠柱状图以便更清晰地比较趋势。

---

## 📊 步骤与代码说明

### Step 1：读取数据并进行异常处理
```python
df = pd.read_csv("superstore_sales.csv", encoding="ISO-8859-1")
```
我们在读取数据时遇到了编码问题，因此显式设置编码为 `ISO-8859-1`，成功读取文件。

---

### Step 2：创建等频分箱区间
```python
df['Sales_QBin'] = pd.qcut(df['Sales'], q=5)
```
通过 `pd.qcut()` 方法将销售额分为 5 个区间，每个区间包含相同数量的订单。这与 `cut()` 的等距切分不同，更适合探索分布密度不均的数据。

---

### Step 3：按区间与商品类别分组，统计数量
```python
bin_category_counts = df.groupby(['Sales_QBin', 'Category']).size().unstack().fillna(0)
```
我们按 `Sales_QBin` 和 `Category` 分组后 `.size()` 统计订单数量，再 `unstack()` 将 `Category` 转为列，方便绘图。

---

### Step 4：绘制堆叠柱状图
```python
bin_category_counts.plot(kind='barh', stacked=True, figsize=(10, 6),
                         color=['#f4a582', '#92c5de', '#d6604d'])
plt.title("不同销售额区间中各商品类别的订单数量（等频分箱）")
plt.xlabel("订单数量")
plt.ylabel("销售额区间")
plt.grid(True, axis='x', linestyle='--', alpha=0.6)
plt.legend(title='Category')
plt.tight_layout()
plt.show()
```

---

## ✅ 结果展示

下图展示了不同销售额区间内，三类商品（家具、办公用品、科技）所占订单数量比例：

![堆叠柱状图](day11_qcut_barh_chart.png)

---

## 📝 分析总结

- 不同销售额区间中，低销售额区间（左侧）中办公用品订单占比较高；
- 随着销售额上升，科技产品占比逐渐增加；
- 家具在所有区间中均衡分布但占比较小。

通过这种方式，我们能够直观理解销售额与商品类别的关系，为后续客户画像与产品组合优化提供支持。

