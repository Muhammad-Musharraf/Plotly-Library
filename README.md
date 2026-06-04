<div align="center">

# 📊 Plotly Library — Interactive Data Visualization

### A complete, hands-on guide to building interactive charts and dashboards with Plotly in Python

[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Plotly](https://img.shields.io/badge/Plotly-5.x-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)](https://plotly.com/python/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![Colab](https://img.shields.io/badge/Open%20in%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/Muhammad-Musharraf/Plotly-Library/blob/main/Plotly_YouTube.ipynb)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)

<br/>

> *From static matplotlib plots to fully interactive Plotly dashboards — learn every major chart type with real datasets, clean code, and practical examples.*

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Repository Structure](#-repository-structure)
- [Charts & Visualizations Covered](#-charts--visualizations-covered)
- [Key Features](#-key-features)
- [Datasets Used](#-datasets-used)
- [Getting Started](#-getting-started)
- [Prerequisites](#-prerequisites)
- [Notes & Cheat Sheet](#-notes--cheat-sheet)
- [Contributing](#-contributing)
- [Author](#-author)

---

## 🚀 Overview

This repository is the official companion notebook for the **Plotly YouTube tutorial series** by **Muhammad Musharraf**. It teaches data visualization from the ground up — starting with simple line plots and progressing to multi-trace figures, bubble charts, matrix plots, and more.

The notebook directly compares **Matplotlib → Seaborn → Plotly**, so you can see exactly why Plotly's interactive, web-ready charts are a step above static alternatives.

**What makes this different:**
- Side-by-side comparison of Matplotlib, Seaborn, and Plotly for the same chart
- Both `plotly.express` (high-level) and `plotly.graph_objects` (low-level) APIs are covered
- Real-world datasets (`tips`, `gapminder`) used throughout — not just toy examples
- Progressive complexity: every concept builds on the previous one

---

## 📁 Repository Structure

```
Plotly-Library/
│
├── 📓 Plotly_YouTube.ipynb       # Main tutorial notebook (all chart types)
│
├── 📂 Notes/
│   └── Plotly cheat sheet.pdf    # Quick-reference guide for Plotly syntax
│
└── README.md
```

---

## 📊 Charts & Visualizations Covered

### 1. 📈 Line Charts
The notebook opens by contrasting three libraries on the same data, then dives deep into Plotly line charts.

```python
# plotly.express — quick and clean
fig = px.line(x=x, y=y, title='Line Graph')

# plotly.graph_objects — full control
fig = go.Figure(go.Scatter(x=x, y=y))
fig.update_layout(title='Line-Graph', xaxis_title='X Axis', yaxis_title='Y Axis')
```

**Concepts covered:**
- `px.line` vs `go.Scatter`
- Adding axis titles and chart titles via `update_layout`
- Multi-trace line charts with `add_trace()`
- Display modes: `lines`, `markers`, `lines+markers`
- Real-world usage with the Gapminder dataset (life expectancy by country/continent)

---

### 2. 🫧 Scatter & Bubble Charts

```python
# Scatter with color grouping
fig = px.scatter(df, x='total_bill', y='tip', color='day', size='size')

# Bubble chart (log scale)
fig = px.scatter(df, x='total_bill', y='tip', color='day', size='size', log_x=True)
```

**Concepts covered:**
- Basic scatter plots with `px.scatter` and `go.Scatter`
- Encoding a third variable with `color`
- Bubble charts using `marker_size` and `size`
- Hover text customization (`hover_data`, `text`)
- Logarithmic axes

---

### 3. 📊 Bar Charts

```python
# Vertical bar with color grouping
fig = px.bar(data, x='day', y='total_bill', color='smoker')

# Horizontal bar chart
fig = px.bar(data_tips, x='tip', y='smoker', orientation='h', color='day')
```

**Concepts covered:**
- Vertical and horizontal bar charts
- Grouping and stacking with `color`
- Filtering data with `.query()` before plotting
- Conditional filtering with pandas boolean indexing
- Rich hover tooltips with `hover_data`

---

### 4. 🥧 Pie Charts

```python
fig = px.pie(data_tips, values='total_bill', names='day',
             color_discrete_sequence=px.colors.sequential.RdBu)
```

**Concepts covered:**
- Basic pie charts with `px.pie`
- Custom color palettes (`px.colors.sequential.RdBu`)
- Adding `color` dimension to pie slices

---

### 5. 📦 Box Plots

A box plot is constructed from five key statistical values:

| Element | Description |
|---------|-------------|
| Bottom whisker | Smallest non-outlier value |
| Q1 | First quartile (25th percentile) |
| Median | Second quartile (50th percentile) |
| Q3 | Third quartile (75th percentile) |
| Top whisker | Largest non-outlier value |

```python
# Notched box plot — shows confidence interval around median
fig = px.box(data_tips, x='day', y='total_bill', color='smoker', notched=True)
```

**Concepts covered:**
- Standard and notched box plots
- Color grouping by categorical variable
- Multi-variable breakdown (day × smoker × total_bill)

---

### 6. 📉 Histograms

```python
# Histogram with marginal distribution overlay
fig = px.histogram(data_tips, x='total_bill', y='tip', color='day', marginal='violin')
```

**Marginal plot options:**

| Option | Description |
|--------|-------------|
| `'rug'` | Individual data point ticks along the axis |
| `'box'` | Box plot overlay above the histogram |
| `'violin'` | Violin plot overlay above the histogram |

**Concepts covered:**
- Basic histograms with `px.histogram`
- Color-grouped histograms
- All four `marginal` options: `rug`, `box`, `violin`, default
- Full-column hover with `hover_data=data_tips.columns`

---

### 7. 🔲 Scatter Matrix (Pair Plot)

```python
fig = px.scatter_matrix(data,
                        dimensions=['total_bill', 'tip', 'size'],
                        color='sex')
```

**Concepts covered:**
- Pairwise scatter plots across multiple numerical features
- Color encoding by category (`sex`, `day`)
- Full matrix using all columns: `dimensions=data.columns`
- Custom sizing with `width` and `height`

---

### 8. ⚙️ Plotly APIs: Express vs Graph Objects

| Feature | `plotly.express` | `plotly.graph_objects` |
|---------|-----------------|----------------------|
| Syntax | High-level, concise | Low-level, verbose |
| Flexibility | Moderate | Full control |
| Best for | Quick exploration | Custom, production charts |
| Multi-trace | Limited | `add_trace()` per trace |
| Layout control | `update_layout()` | `update_layout()` |

Both APIs are used throughout the notebook so you understand when to reach for each.

---

## ✨ Key Features

- 🔁 **Side-by-side comparison** — Matplotlib → Seaborn → Plotly for the same chart type
- 🎨 **Interactive by default** — hover, zoom, pan, and filter built into every chart
- 📡 **Multi-trace figures** — overlay multiple datasets on one chart with `add_trace()`
- 🔍 **Data filtering in plots** — `.query()` and boolean indexing before plotting
- 🎯 **Hover customization** — rich tooltips showing exactly the data you want
- 📐 **Layout control** — axis titles, chart titles, figure sizing, color sequences
- 📊 **Statistical plots** — box plots with quartile explanation, notched confidence intervals
- 🌍 **Real datasets** — `tips` and `gapminder` from `plotly.express.data`

---

## 🗂️ Datasets Used

| Dataset | Source | Description |
|---------|--------|-------------|
| `tips` | `px.data.tips()` | Restaurant tipping data (244 rows) — `total_bill`, `tip`, `sex`, `smoker`, `day`, `time`, `size` |
| `gapminder` | `px.data.gapminder()` | World development indicators — `country`, `continent`, `year`, `lifeExp`, `pop`, `gdpPercap` |
| Custom arrays | Inline | `x`, `y` lists and NumPy arrays for foundational chart examples |

---

## 🛠️ Getting Started

### ▶️ Option A — Google Colab *(Zero setup, recommended)*

Click the badge to open the notebook directly in Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Muhammad-Musharraf/Plotly-Library/blob/main/Plotly_YouTube.ipynb)

Then go to `Runtime → Run all`. Plotly is pre-installed in Colab — no additional setup needed.

---

### 💻 Option B — Local Setup

**1. Clone the repository**

```bash
git clone https://github.com/Muhammad-Musharraf/Plotly-Library.git
cd Plotly-Library
```

**2. Create a virtual environment**

```bash
# macOS / Linux
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

**3. Install dependencies**

```bash
pip install plotly pandas numpy matplotlib seaborn jupyter
```

**4. Launch the notebook**

```bash
jupyter notebook Plotly_YouTube.ipynb
```

---

## 📦 Prerequisites

| Package | Version | Purpose |
|---------|---------|---------|
| `plotly` | ≥ 5.0 | Interactive visualizations (`express` + `graph_objects`) |
| `pandas` | ≥ 1.4 | Data manipulation and filtering |
| `numpy` | ≥ 1.22 | Numerical arrays for custom data |
| `matplotlib` | ≥ 3.5 | Comparison baseline (static plots) |
| `seaborn` | ≥ 0.12 | Comparison baseline (statistical plots) |
| `jupyter` | ≥ 1.0 | Notebook environment |

Install everything at once:

```bash
pip install plotly pandas numpy matplotlib seaborn jupyter
```

---

## 📄 Notes & Cheat Sheet

The `Notes/` folder contains a **Plotly Cheat Sheet PDF** — a quick-reference card covering the most commonly used syntax, parameters, and chart types. Keep it open alongside the notebook while learning.

```
Notes/
└── Plotly cheat sheet.pdf
```

---

## 🗺️ Suggested Learning Path

Follow this sequence for the best progression through the notebook:

```
1. Line Charts           →  px.line + go.Scatter basics
         ↓
2. Multi-Trace Figures   →  add_trace(), display modes
         ↓
3. Scatter & Bubble      →  color, size, hover_data
         ↓
4. Bar Charts            →  vertical, horizontal, grouped, filtered
         ↓
5. Pie Charts            →  values, names, color palettes
         ↓
6. Line + Real Data      →  Gapminder, continent filtering
         ↓
7. Box Plots             →  statistical summary, notched
         ↓
8. Histograms            →  marginal: rug, box, violin
         ↓
9. Scatter Matrix        →  pairwise relationships, full matrix
```

---

## 🤝 Contributing

Contributions are welcome! To add a new chart type, fix a bug, or improve explanations:

1. **Fork** the repository
2. **Create a branch**: `git checkout -b feature/treemap-chart`
3. **Commit** your changes: `git commit -m "Add: treemap chart with real estate data"`
4. **Push**: `git push origin feature/treemap-chart`
5. **Open a Pull Request** with a clear description of what was added

Please keep notebooks clean, well-commented, and consistent with the existing style.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE). You are free to use, adapt, and share the code with proper attribution.

---

## 👨‍💻 Author

<div align="center">

**Muhammad Musharraf**
*Data Scientist & ML Educator*

[![GitHub](https://img.shields.io/badge/GitHub-Muhammad--Musharraf-181717?style=for-the-badge&logo=github)](https://github.com/Muhammad-Musharraf)
[![YouTube](https://img.shields.io/badge/YouTube-Subscribe-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtube.com)

</div>

---

<div align="center">

### ⭐ Found this helpful? Star the repo — it helps others discover it!

*Built with ❤️ for the data visualization community*

</div>
