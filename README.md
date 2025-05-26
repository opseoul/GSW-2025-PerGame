# 🏀 Golden State Warriors Player Performance Analysis (2025)

This project analyzes Golden State Warriors player performance using publicly available per-game statistics from the 2025 NBA season. The goal is to identify top performers, explore player efficiency, and segment players into distinct roles using clustering techniques.

---

## 📊 Dataset

- **Source**: [Basketball Reference – GSW 2025](https://www.basketball-reference.com/teams/GSW/2025.html)
- **Format**: Per-game player stats (CSV format)
- **Features include**:
  - Player: Name
  - Pos: Position
  - MP: Minutes per Game
  - PTS: Points per Game
  - FG%, AST, TRB, STL, BLK, TOV, and more

---

## 🧼 Data Cleaning

- Removed the **"Team Totals"** row
- Converted relevant performance columns to numeric
- Created custom efficiency metrics:
  - `Scoring_Efficiency = PTS / FGA`
  - `All_Around_Efficiency = PTS + AST + TRB + STL + BLK`

```python
# Drop team total row
df = df[df["Player"] != "Team Totals"]

# Convert numeric columns
for col in df.columns[3:-2]:
    df[col] = pd.to_numeric(df[col], errors='coerce')

🌟 Top Player Metrics
🔥 Top 5 – Scoring Efficiency
python
Copy
Edit
df[["Player", "Scoring_Efficiency"]]
   .sort_values(by="Scoring_Efficiency", ascending=False)
   .head(5)
🔁 Top 5 – All-Around Efficiency
python
Copy
Edit
df[["Player", "All_Around_Efficiency"]]
   .sort_values(by="All_Around_Efficiency", ascending=False)
   .head(5)
📊 Visualizations
🏀 Top 10 Scorers
python
Copy
Edit
sns.barplot(data=top_scorers, x="PTS", y="Player", palette="viridis")
⏱️ Minutes vs Points (Colored by Position)
python
Copy
Edit
df_clean = df[['MP', 'PTS', 'Pos']].dropna()
df_clean['Pos'] = df_clean['Pos'].astype(str).str.strip()
sns.scatterplot(data=df_clean, x="MP", y="PTS", hue="Pos")
📈 Correlation Heatmap
python
Copy
Edit
sns.heatmap(df_clean.corr(numeric_only=True), annot=True, cmap="coolwarm")
🧍 Starters vs Bench – Points Comparison
python
Copy
Edit
df['Role'] = df['GS'].apply(lambda x: 'Starter' if x > 30 else 'Bench')
sns.boxplot(data=df, x='Role', y='PTS')
🔍 Player Role Clustering (KMeans)
🎯 Objective
Use clustering to segment players into:

High-Impact Starters

Role Players

Bench/Development

📊 Features Used for Clustering
python
Copy
Edit
features = ['MP', 'PTS', 'AST', 'TRB', 'FG%', 'STL', 'BLK', 'TOV']
⚙️ Clustering Workflow
python
Copy
Edit
scaler = StandardScaler()
X_scaled = scaler.fit_transform(df_cluster)

kmeans = KMeans(n_clusters=3, random_state=42)
df_cluster['Cluster'] = kmeans.fit_predict(X_scaled)

label_map = {
    0: 'High-Impact Starter',
    1: 'Role Player',
    2: 'Bench/Development'
}
df_cluster['Role'] = df_cluster['Cluster'].map(label_map)
📍 Visualization
python
Copy
Edit
sns.scatterplot(data=df_cluster, x='MP', y='PTS', hue='Role', palette='Set2')
📌 Summary
This analysis provides a data-driven breakdown of the Golden State Warriors’ roster using advanced metrics and clustering. It helps uncover player strengths, roles, and potential development paths for lineup optimization and coaching decisions.

📁 Files Included
GSW_2025_PerGame.csv – Raw dataset

GSW_Player_Analysis.ipynb – Full Jupyter Notebook

README.md – Project overview

🧰 Tools Used
Languages: Python (Pandas, NumPy)

Visualization: Seaborn, Matplotlib

Modeling: scikit-learn (KMeans, StandardScaler)

Notebook: Jupyter

Source: Basketball Reference – GSW 2025

