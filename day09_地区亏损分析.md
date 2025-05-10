# Day 9 地区亏损分析：统计各地区订单分布与亏损情况

今天我们以亏损编辑集（`loss_state_df`）为分析对象，从地区（`Region`）角度定量评订单分布和总亏损情况。分为两步：

---

## 一、各地区在亏损订单中的出现次数

我们先使用 `.value_counts()` 统计各地区在亏损订单中出现的频次：

```python
region_counts = loss_state_df['Region'].value_counts()
```

随后绘制柱状图展示：

- Central 出现最多，West 最少
- 可能反映了中部地区订单量或运营异常更多

---

## 二、各地区的总亏损金额

我们使用 `.groupby().sum()` 对 `Profit` 进行地区聚合，得到总亏损金额并排序：

```python
region_profit = loss_state_df.groupby('Region')['Profit'].sum().sort_values()
```

随后绘制横向柱状图观察亏损程度：

- Central 亏损最严重（-38,000+）
- East 次之（-32,000+）

---

## 📌 分析结论：

- **中部（Central）** 是目前订单最多且亏损最严重的地区；
- 建议在该区域深入挖掘原因（如客户、产品、运输方式等），作为后续优化重点；
- 西部（West）订单较少但也存在亏损，需保持关注。

