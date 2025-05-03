
# 📊 数据分析项目 Day 4：利润占比图表分析

本日目标是使用 `pivot_table`、比例计算、堆叠柱状图 来分析**各商品小类在不同地区的利润占比**。

---

## ✅ 任务概览

我们将：

1. 创建交叉表 `pivot_table` 得到商品小类 × 地区的利润汇总
2. 计算每一行的总和
3. 用 `.div(..., axis=0)` 算出各地区占比
4. 使用 `pandas.plot` 的堆叠柱状图 `.plot(kind='barh', stacked=True)` 画出利润占比图

---

## 📌 步骤详解

### 第 1 步：构建交叉表

```python
pivot_profit = df.pivot_table(
    index='商品小类',
    columns='地区',
    values='利润',
    aggfunc='sum'
)
```

输出示例：

| 商品小类 | Central | East | South | West |
|----------|---------|------|-------|------|
| Phones   | 12323   | 12315| 10767 | 9111 |

---

### 第 2 步：计算每行总和（每个小类的总利润）

```python
pivot_profit_sum = pivot_profit.sum(axis=1)
```

---

### 第 3 步：计算每个小类在不同地区的利润占比

```python
pivot_profit_ratio = pivot_profit.div(pivot_profit_sum, axis=0)
```

---

### 第 4 步：绘图（堆叠横向柱状图）

```python
pivot_profit_ratio.plot(
    kind='barh',
    stacked=True,
    figsize=(10, 6),
    cmap='Pastel1'  # 或其他 colormap
)
plt.title('各商品小类在不同地区的利润占比')
plt.xlabel('占比')
plt.ylabel('商品小类')
plt.tight_layout()
plt.show()
```

---

## 📈 图表说明

这张图表示：

- 每一行代表一个商品小类
- 不同颜色的块代表不同地区的占比
- 越长的块 → 说明该地区在该商品类别的利润占比越高

---

## 🎓 总结 & 语法复习

| 概念 | 示例 | 说明 |
|------|------|------|
| `pivot_table()` | `df.pivot_table(index, columns, values, aggfunc)` | 创建交叉表（透视表） |
| `.sum(axis=1)` | `df.sum(axis=1)` | 每一行求和（横向加总） |
| `.div(..., axis=0)` | `df.div(total, axis=0)` | 每行元素除以该行总和 |
| `.plot(kind='barh', stacked=True)` | `df.plot(...)` | Pandas 内置绘图函数 |

---

✅ Day 4 完成！下一步将进入 Day 5，更复杂的时间趋势分析 🔍。
