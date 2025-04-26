
## ✅ Day 3 复盘总结：图表可视化基础 & 销售分析

---

### 🎯 学习目标
- 掌握常见的销售数据分析方法
- 理解分组汇总、时间处理与图表绘制
- 学会用 `Pandas + Matplotlib + Seaborn` 进行基础可视化

---

### 📊 图表①：销售金额分布直方图

#### 🔍 目的
分析销售额的整体分布状态，有无极端高额订单。

#### ✅ 技术点
```python
sns.histplot(df['sales'], bins=30, kde=True)
```
- `sns.histplot()`：绘制直方图（自动分箱统计）
- `bins=30`：分成 30 个区间
- `kde=True`：加入平滑的密度曲线

---

### 📊 图表②：不同地区的销售额 & 利润柱状图

#### 🔍 目的
比较 Central / East / South / West 四个地区的总销售与总利润。

#### ✅ 技术点
```python
region_sales = df.groupby('region')[['sales', 'profit']].sum()
region_sales.plot(kind='bar')
```
- `.groupby('region')`：按地区分组
- `[[]]`：取出多个列
- `.sum()`：分别汇总
- `.plot(kind='bar')`：画柱状图

---

### 📈 图表③：每月销售趋势折线图

#### 🔍 目的
观察销售额随月份的波动趋势，有无周期性变化。

#### ✅ 技术点
```python
df['order_month'] = df['order_date'].dt.to_period('M')
monthly_sales = df.groupby('order_month')['sales'].sum()
monthly_sales.plot(kind='line')
```
- `.dt.to_period('M')`：将日期转成年月格式
- `groupby('order_month')`：按月分组
- `.plot(kind='line')`：折线图显示趋势

---

### 📊 图表④：商品小类利润横向柱状图

#### 🔍 目的
查看哪些子类别最赚钱，哪些亏损。

#### ✅ 技术点
```python
subcategory_profit = df.groupby('Sub-Category')['profit'].sum().sort_values()
subcategory_profit.plot(kind='barh', color='skyblue')
```
- `'Sub-Category'`：注意列名大小写！
- `.sort_values()`：排序后更清晰
- `'barh'`：横向柱状图

---

### 🧠 常见问题汇总
- ❗ 列名错误：检查拼写、大小写、横杠 vs 下划线
- ❗ 中文乱码：使用 `fontproperties=myfont` 手动设字体
- ❗ 图不显示：`plt.show()` 一定要加
- ❗ 变量不存在：检查是否未先运行前面的代码块

---

### 📚 学会了什么？
- 使用 `.groupby()` 进行汇总分析
- 时间列 `.dt` 相关处理（转月、转年）
- `plot()` 与 `sns.histplot()` 的区别与应用
- 识别数据图像的趋势和特征

---

### ✅ 下一步建议
- 再手动完整复现一次四张图，加深记忆
- 整理常见图表模板：直方图、柱状图、折线图、横向柱状图
- 进入 Day 4：图表组合 + 多维分析 + 总结报告

你真的做得很好💪 有任何一部分不会，我们都可以继续精讲🔥
