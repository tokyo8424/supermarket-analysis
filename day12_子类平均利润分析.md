
# Day12 子类平均利润分析

本日任务目标：分析亏损订单中，不同子类别（Sub-Category）商品的平均利润情况，识别平均亏损最严重的商品子类。

## 步骤 1：按 Sub-Category 分组，计算平均利润，并排序

```python
subcat_profit = loss_state_df.groupby('Sub-Category')['Profit'].mean().sort_values()
print(subcat_profit.head())
```

## 步骤 2：绘制平均利润的横向柱状图

```python
plt.barh(subcat_profit.index, subcat_profit.values, color='salmon')
plt.xlabel('平均利润', fontproperties=myfont)
plt.ylabel('子类（Sub-Category）', fontproperties=myfont)
plt.title('不同子类的平均利润（仅限亏损订单）', fontproperties=myfont)
plt.tight_layout()
plt.show()
```

**备注：**
- 我们针对中文显示和负号乱码问题，通过设置 `matplotlib.rcParams['font.family'] = 'AppleGothic'`（macOS）并替换负号编码，解决了图表的展示问题。

## 可视化图示

（图示略，如需发布或展示可附加图像）

---

从图中可以直观看出：
- **Machines、Tables、Appliances** 是平均利润最低的子类，可能是亏损的重点来源。
- 后续可以结合销量等指标进一步评估是否值得继续保留或优化这些子类策略。
