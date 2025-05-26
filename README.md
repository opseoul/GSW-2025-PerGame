# 🏀 Golden State Warriors Player Performance Analysis (2025)

This project analyzes Golden State Warriors player performance using publicly available per-game statistics from the 2025 NBA season. The goal is to identify top performers, explore player efficiency, and segment players into distinct roles using clustering techniques.

---

## 📊 Dataset

- **Source**: [Basketball Reference – GSW 2025](https://www.basketball-reference.com/teams/GSW/2025.html)
- **Format**: Per-game player stats
- **Columns include**: Player, Position, Minutes Played (MP), Points (PTS), Field Goal %, Assists (AST), Rebounds (TRB), Steals (STL), Blocks (BLK), Turnovers (TOV), and more.

---

## 🧼 Data Cleaning

- Removed the `"Team Totals"` row
- Converted numeric columns using `pd.to_numeric`
- Created two custom metrics:
  - **Scoring Efficiency** = PTS ÷ FGA
  - **All-Around Efficiency** = PTS + AST + TRB + STL + BLK

---

## 🌟 Top Player Metrics

### 🔥 Top 5 Scorers by Efficiency
Players ranked by their points scored per field goal attempt.

### 🧮 Top 5 All-Around Players
Players contributing across scoring, assists, rebounds, steals, and blocks.

---

## 📊 Visualizations

### 🏀 Top 10 Scorers
A horizontal bar chart showing the 10 highest-scoring players on the team.

### ⏱️ Minutes vs Points (Colored by Position)
A scatter plot illustrating how playing time correlates with scoring, with points colored by player position (PG, SG, SF, PF, C).

### 📈 Correlation Heatmap
A heatmap showing correlations between major performance indicators like points, assists, rebounds, etc.

### 🧍 Starter vs Bench Comparison
A box plot comparing points scored by starters vs bench players.

---

## 🔍 KMeans Player Role Clustering

### 🎯 Objective
Segment players into meaningful performance-based roles:
- **High-Impact Starters**
- **Role Players**
- **Bench/Development**

### ⚙️ Features Used for Clustering
- Minutes Played (MP)
- Points Scored (PTS)
- Assists (AST)
- Rebounds (TRB)
- Field Goal % (FG%)
- Steals (STL)
- Blocks (BLK)
- Turnovers (TOV)

### 🧪 Clustering Process
- Missing values were dropped.
- Features were scaled using `StandardScaler`.
- KMeans with 3 clusters was applied to segment players.
- Clusters were mapped to interpretive labels:
  - Cluster 0 → High-Impact Starter
  - Cluster 1 → Role Player
  - Cluster 2 → Bench/Development

### 📍 Visualization
Scatter plot of Minutes vs Points with players colored by cluster-defined role.

---

## 📅 Summary

This project provides a data-driven view of Golden State Warriors’ player performance during the 2025 NBA season. It highlights key players, reveals correlations, and segments the roster into roles that can inform coaching, rotations, and player development.

---

## 📁 Files Included

- `GSW_2025_PerGame.csv` – Raw per-game statistics
- `GSW_Player_Analysis.ipynb` – Jupyter Notebook with full analysis
- `README.md` – Project overview

---

## 🧰 Tools Used

- **Language**: Python
- **Libraries**: Pandas, Seaborn, Matplotlib, scikit-learn
- **Environment**: Jupyter Notebook
- **Data Source**: [Basketball Reference – GSW 2025](https://www.basketball-reference.com/teams/GSW/2025.html)
