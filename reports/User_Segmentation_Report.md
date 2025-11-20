# 📊 电商用户画像与用户价值分析报告  
（Ecommerce User Segmentation & Value Analysis Report）

---

## 1. 项目背景

本项目基于电商消费者行为数据，通过以下方法构建完整的用户画像体系：

- **KMeans 行为聚类模型**
- **RFM 用户价值模型**
- **行为 × 价值 的多维标签体系**
- **可视化分析（雷达图、热力图、旭日图、树状图）**

目标是理解不同消费者群体的行为特点与价值差异，为企业运营提供有针对性的用户策略。

---

## 2. 数据概览

- 数据量：**1000 条记录，28 个字段**
- 包含用户属性、购买行为、消费金额、参与度、满意度等信息
- 关键字段示例：Age、Frequency、Brand_Loyalty、Purchase_Amount、Time_of_Purchase 等

数据清洗工作包括：

- 金额字段去除 `$` → 转为 float
- 日期解析为 datetime
- One-Hot 编码分类字段
- 数值标准化处理

---

## 3. KMeans 行为聚类

### 3.1 特征工程

构建行为类变量（部分）：

| 特征名 | 含义 |
|--------|------|
| Monetary | 本次消费金额 |
| Frequency | 购买频率 |
| Loyalty_Score | 品牌忠诚度 + 满意度 |
| Engagement | 是否参与优惠 + 是否会员 |
| Product_Rating | 产品评分 |
| Return_Rate | 退货率 |
| Time_Spent_on_Research | 决策前研究时间 |
| Time_to_Decision | 决策时长 |

分类变量经过 One-Hot 编码后进入模型。

---

### 3.2 聚类结果总结

最终得到 **5 类用户行为分群**：

- **Cluster 0：深度研究型用户**  
  研究时间长、决策慢、信息敏感度高  
- **Cluster 1：高参与型用户**  
  积极使用优惠、活动参与度高  
- **Cluster 2：价格敏感型用户**  
  Monetary 低，折扣敏感度高  
- **Cluster 3：潜在流失型用户**  
  满意度与活跃度偏低  
- **Cluster 4：年轻高潜用户**  
  年龄低、成长潜力高

---

### 3.3 聚类可视化

#### 🟦 聚类雷达图

<img width="2400" height="2400" alt="cluster_radar" src="https://github.com/user-attachments/assets/05da8533-b8dc-4b3a-a6d6-bc384ca59642" />


#### 🟦 聚类特征均值柱状图


<img width="3570" height="4605" alt="cluster_feature_bars" src="https://github.com/user-attachments/assets/d06bbf02-2cc0-45d5-ba37-adb42eadc4a8" />


## 4. RFM 用户价值模型

### 4.1 指标定义

- **R（Recency）**：距最近一次购买的天数  
- **F（Frequency）**：累计购买频率  
- **M（Monetary）**：累计消费金额  

R、F、M 各维度按五分位打分（1~5）。

---

### 4.2 用户价值分层结果

| RFM 总分 | 价值区间 |
|----------|----------|
| 13–15 | VIP 超高价值用户 |
| 10–12 | 高价值用户 |
| 7–9 | 中价值用户 |
| 4–6 | 低价值用户 |
| 3 | 潜在流失用户 |

### 分层统计如下：

- 中价值用户：458  
- 高价值用户：304  
- 低价值用户：159  
- VIP 超高价值：71  
- 潜在流失：8  

---

### 4.3 RFM 可视化

#### 🟥 RFM 热力图


<img width="1866" height="1582" alt="RFM_heatmap" src="https://github.com/user-attachments/assets/c6644ce6-f058-4b62-8e1b-5c565e0a07ee" />

#### 🟩 RFM 雷达图



<img width="2039" height="1979" alt="RFM_radar" src="https://github.com/user-attachments/assets/22c4f3ab-d60c-467c-a053-47295fb1e92b" />


## 5. 多维用户标签体系（行为 × 价值）

将：

- **行为聚类（5 类）**
- **价值模型（5 类）**

结合生成 **25 种最终用户标签**：
如：

- VIP · 深度研究型用户  
- 高价值 · 潜在流失行为型用户  
- 中价值 · 价格敏感型用户  

输出文件：  
`user_multi_dimension_segment.csv`

---

## 6. 多维标签可视化

### 6.1 旭日图（人数维度）
[sunburst_by_count.html](https://github.com/user-attachments/files/23654984/sunburst_by_count.html)


### 6.2 树状图（金额贡献）

![Treemap Monetary](./figures/treemap_by_monetary.png)

---

## 7. 用户洞察总结（Insights）

### ⭐ 高价值用户（VIP + 高价值）
- 高频购买
- 忠诚度强
- 金额贡献最高

**策略：** 专属优惠、会员权益升级、提前购。

---

### ⭐ 中价值用户（人数最多）
- 消费稳定
- 是最主要用户基盘

**策略：** 提升复购、推荐组合商品。

---

### ⭐ 价格敏感型用户
- 金额低但对优惠敏感

**策略：** 满减、限时折扣、优惠力度展示。

---

### ⭐ 深度研究型用户
- 决策时间长

**策略：** 增强内容信息、评价、对比功能。

---

### ⭐ 潜在流失用户
- R 高、F&M 低

**策略：** 唤醒营销、短信提醒、优惠激励。

---

## 8. 结论

通过 **聚类 + RFM + 标签体系** 构建出完整的电商用户画像系统，使得业务可以：

- 精准定位用户价值  
- 针对不同群体执行运营策略  
- 优化营销资源投入  
- 为商品推荐与会员体系提供依据  

