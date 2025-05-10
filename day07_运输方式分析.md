
# Day 7 运输方式分析：损亏订单中运输方式的分布和衡量

本日分析目标是：**从已识别的亏损订单中，探索不同运输方式的分布、平均利润和平均销售额**，找出可能的成本控制优化方向。

---

## 一、订单分布：各运输方式在损亏订单中的次数

通过 `.value_counts()` 对 `loss_state_df['Ship Mode']` 进行计数：

| Ship Mode       | Count |
|----------------|-------|
| Standard Class | 2342  |
| Second Class   | 691   |
| First Class    | 637   |
| Same Day       | 208   |

✅ 可视化如下：

- 标准运送方式占比最高，但并不一定代表最不合理。

---

## 二、运输方式平均亏损比较

对 `Profit` 按运输方式进行 `.groupby()` 与 `.mean()`，并按平均值升序排列：

| Ship Mode       | 平均亏损 |
|----------------|----------|
| Standard Class | -26+     |
| Same Day       | -21+     |
| First Class    | -19+     |
| Second Class   | -17+     |

✅ 结论：平均亏损最高的是 Standard Class，虽然它是最常用的运输方式。

---

## 三、运输方式平均销售额比较

对 `Sales` 按运输方式 `.groupby()` 后取均值：

| Ship Mode       | 平均销售额 |
|----------------|------------|
| Second Class   | 196.2      |
| Same Day       | 194.8      |
| Standard Class | 183.4      |
| First Class    | 157.2      |

📌 观察：
- Second Class 平均销售额最高，但平均亏损相对较低；
- Standard Class 平均销售额较低，亏损反而最高，**可能存在过度优惠或效率问题**。

---

## ✅ 分析小结

- **Standard Class 虽然最常用，但平均亏损最高，需重点关注其成本结构**；
- **Second Class 综合表现最好：亏损低、销售高**；
- 后续可深入分析：是否因运输时效、产品类型、或地区差异所致。

---

*以上为 Day 7 分析内容，下一步将进行订单时效相关探索。*
