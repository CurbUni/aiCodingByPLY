### 📄 3. 项目说明文档 (README.md)
用于覆盖你们仓库原有的 README，供评委查阅。
**README.md**
```markdown
# 📡 5G 信号 3D 可视化看板 (Code with AI 挑战赛作品)

本项目是基于 Streamlit 框架，在 AI Coding Agent 的辅助下极速搭建的 5G 路测信号可视化 Web 看板。旨在展示如何在摒弃繁杂前端代码编写的情况下，通过自然语言驱动快速完成数据加载、清洗、多维图表展示与 3D 空间渲染。

## 🌟 核心功能特性

- **🟢 基础关卡达成**
  - **动态地图分布**：基于 CSV 中的经纬度渲染基站落点，并依据 RSRP 信号强度进行智能着色分类（大于 -90dBm 绿、小于 -110dBm 红、居中黄）。
  - **业务概览图表**：集成了终端类型（Smartphone, CPE, IoT）占比饼图与各频段（n28, n41, n78 等）基站数量柱状图。
- **🟡 进阶关卡达成**
  - **全局联动筛选**：左侧边栏支持多频段过滤及 RSRP 滑动区间过滤，操作后 3D 地图与概览图表实现毫秒级实时刷新。
  - **极客 3D 视觉体验**：摒弃传统二维平面，采用 PyDeck 的 `ColumnLayer` 将路测点 3D 柱状化，其高度由 Download_Mbps 直接映射，实现信号质量的空间可视化。
  - **工程化交付**：核心代码包含完整 Python 类型提示与函数注释，并提供基于 `pytest` 的单元测试 `test_app.py`。

## 🚀 快速启动指南

1. **安装环境依赖**：
   在终端中运行以下命令安装必需的库：
   ```bash
   pip install -r requirements.txt

```
 2. **启动 Streamlit 服务**：
   ```bash
   streamlit run app.py
   
   ```
 3. **运行单元测试**：
   ```bash
   pytest test_app.py
   
   ```
```

---

### 🤖 4. Agent 交互日志 (`AI_PROMPTS.md`)

评委重点考察的交付物，记录了你“指使”AI的工作流。

**`AI_PROMPTS.md`**
```markdown
# AI Coding Agent 交互验收日志

本记录展现了我们利用大模型极速构建 5G 看板的交互步骤。

**Prompt 1 (基础框架建立)：**
> “请使用 Streamlit 帮我写一个 5G 信号看板。要求：1. 读取目录下的 `signal_samples.csv`。 2. 网页需要有一个大标题。 3. 在主体区域使用 st.map 或 pydeck 渲染交互地图，并将数据中的经度、纬度打点在地图上。核心要求：大于 -90dBm 的点标记为绿色，小于 -110dBm 的为红色，中间的为黄色。4. 地图下方，生成一个饼图展示 TerminalType 的比例，一个柱状图展示各个 Band 的基站数量。”

**Prompt 2 (进阶筛选与联动)：**
> “代码跑通了！现在我们需要加点料。请在网页左侧生成一个侧边栏（Sidebar）。包含两样东西：1. 多选下拉菜单，用来筛选 Band。2. 一个双向滑动条，用来筛选 RSRP_dBm 范围。**关键要求**：当我拖动筛选器时，右边刚刚生成的地图和图表必须实时联动更新！”

**Prompt 3 (3D 极客视觉改造)：**
> “平面的打点不够酷炫。请把我刚才地图的部分，重构为 pydeck 的 3D 视角（ColumnLayer）。让信号点变成 3D 柱状体，柱子的高度根据 `Download_Mbps` 这个字段的值来决定，保留之前的 RSRP 颜色逻辑，同时开启 tooltip 显示基站ID和下载速率。视图初始 pitch 调整为 45 度左右以便观看 3D 效果。”

**Prompt 4 (工程规范闭环)：**
> “最后，请你扮演资深架构师，为刚才代码里核心的数据加载和过滤函数补充标准的 docstring 注释，并且给我单独输出一个 `test_app.py`，里面用 pytest 框架对这个过滤函数写两个基础的单元测试。”

```
### 🏁 极速提交流程
为了符合比赛时间戳计分的硬性规定，请在你的本地仓库完成这几步：
 1. 将以上文件存入本地文件夹，并放好 data/signal_samples.csv。
 2. 运行并截图 2-3 张（按照赛题要求补充截图文件 screenshot1.png 等）。
 3. 依次执行完赛指令：
```bash
git add .
git commit -m "feat: complete basic and advanced challenges for 5G dashboard"

# 基础关卡打卡
git tag basic-done
git push origin basic-done

# 进阶关卡打卡
git tag advanced-done
git push origin advanced-done

# 推送主分支代码
git push origin main

```
