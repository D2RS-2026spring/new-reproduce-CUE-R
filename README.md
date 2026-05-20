# 荟萃分析与机器学习揭示氮富集下微生物碳利用效率的关键驱动因素复现

---

## 1. 项目说明
本仓库包含论文《荟萃分析与机器学习揭示氮富集下微生物碳利用效率的关键驱动因素》所使用的数据集和R代码。
研究整合多篇同行评审研究数据，探究氮添加对土壤微生物碳利用效率（CUE）的影响，并采用MetaForest机器学习方法识别影响微生物CUE的核心环境与管理驱动因子。
- 原始数据:https://doi.org/10.5281/zenodo.15535868
- 代码链接:https://doi.org/10.5281/zenodo.15535868
---

## 2. 仓库内容
- extracted_data.csv – 基于已发表研究整理的荟萃分析数据集
- analysis_code.R – 用于数据处理、荟萃回归与MetaForest建模的R脚本
- README.md – 项目说明文档


---

## 3. 数据说明
文件：extracted_data.csv
每一行代表一项来自田间试验的观测（效应量对比），用于分析氮添加对微生物碳利用效率（CUE）的影响。
数据集包含氮处理组与对照组的均值、标准差、样本量，以及环境调节变量。

| 列名 | 说明 |
| ---- | ---- |
| obs | 观测编号，每条记录唯一 |
| Site | 站点编码或研究标识 |
| Latitude | 研究站点纬度（十进制度） |
| Longitude | 研究站点经度（十进制度） |
| tm | 氮处理组微生物CUE均值 |
| ts | 氮处理组CUE标准差 |
| tn | 氮处理组样本量 |
| cm | 对照组微生物CUE均值 |
| cs | 对照组CUE标准差 |
| cn | 对照组样本量 |
| MAP | 年均降水量（mm），分组变量 |
| N_addtion | 氮添加水平（如<100、100–200、>200 kg N ha⁻¹ yr⁻¹），分类变量 |
| pH | 土壤pH |
| MAT | 年均气温（℃） |
| SOC | 土壤有机碳含量（g kg⁻¹） |
| TN | 土壤全氮含量（g kg⁻¹） |
| TP | 土壤全磷含量（g kg⁻¹） |
| CNR | 土壤碳氮比 |
| NPR | 土壤氮磷比 |
| MBC | 微生物生物量碳（mg kg⁻¹） |
| MBN | 微生物生物量氮（mg kg⁻¹） |
| MCNR | 微生物碳氮比（无单位） |

缺失值使用 NA 表示。
## 4. R代码使用说明及项目复现方法
文件：analysis_code.R
编码：UTF-8
软件要求：R 4.2.0 及以上版本

### 所需R包
tidyverse, meta, metafor, metadat, metaforest, caret, broom, ggplot2, ggspatial, RColorBrewer, ggtext, rcartocolor, ggsci, sf

运行脚本前请确保所有包已安装并更新至最新版本。

### 脚本功能与步骤
1. 采样点地图绘制
   基于经纬度可视化研究站点的全球分布
   输出：Figure 1 Geographic distribution of observational field studies included in the meta-analysis.pdf

2. 效应量计算与森林图
   计算对数响应比，拟合随机效应荟萃分析模型
   输出：Figure 2 Forest plot of the effects of nitrogen addition on soil microbial carbon use efficiency.pdf

3. 发表偏倚检验
   绘制漏斗图并进行Egger回归检验
   输出：Figure S1 Funnel plot with regression test for asymmetry.pdf

4. 亚组与调节变量分析
   对降水量（MAP）和氮添加水平进行荟萃回归
   输出：Figure 3 Effects of nitrogen addition on soil microbial carbon use efficiency across precipitation and nitrogen addition levels.pdf
   同时进行亚组效应t检验

5. 连续调节变量回归
   连续变量荟萃回归，含预测区间与QQ图
   输出：Figure 4、Figure S4 回归图与诊断图

6. 机器学习（MetaForest）
   训练MetaForest模型，按重要性排序调节变量
   执行递归特征筛选、参数调优、偏依赖分析
   输出：
   - Figure S2_a、S2_b：收敛图
   - Figure S3：重复变量重要性图
   - Figure S5：预测值与观测值对比图
   - Figure 5、Figure 6：重要性柱状图与偏依赖图

### 项目复现方法
1. 将 analysis_code.R、extracted_data.csv、global.shp 放在工作目录下
2. 在 RStudio 中打开 analysis_code.R
3. 逐步运行脚本，生成所有图表与输出结果

---
## 5. 本文文献引用方式
如使用本数据集或代码，请引用：
Yin, T., et al. (2025). Dataset and code for "Meta-analysis and Machine Learning Reveal Key Drivers of Microbial Carbon Use Efficiency Under Nitrogen Enrichment".

---

## 6. 许可协议
本仓库采用知识共享署名 4.0 国际许可协议（CC BY 4.0）。
您可自由分享和改编本材料，包括用于商业用途，只需注明原作者出处。

---
