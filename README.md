🏀 Golden State Warriors Player Performance Analysis (2025)

This project analyzes Golden State Warriors player performance using publicly available per-game statistics from the 2025 NBA season. The goal is to identify top performers, explore player efficiency, and segment players into distinct roles using clustering.

📊 Dataset

Source: Basketball Reference - GSW 2025 (https://www.basketball-reference.com/teams/GSW/2025.html)

Format: Per-game player stats

Columns include: PTS, MP, FG%, AST, TRB, STL, BLK, TOV, Pos, and more

🔧 Data Cleaning

Removed "Team Totals" row

Converted relevant columns to numeric

Created custom metrics:

Scoring_Efficiency = PTS / FGA

All_Around_Efficiency = PTS + AST + TRB + STL + BLK

# Drop team total row
df = df[df["Player"] != "Team Totals"]

# Convert numeric columns
for col in df.columns[3:-2]:
    df[col] = pd.to_numeric(df[col], errors='coerce')

📊 Top Players

Scoring Efficiency

top_efficiency = df[["Player", "Scoring_Efficiency"]].sort_values(by="Scoring_Efficiency", ascending=False).head(5)

All-Around Efficiency

top_all_around = df[["Player", "All_Around_Efficiency"]].sort_values(by="All_Around_Efficiency", ascending=False).head(5)

🌍 Visualization

🏋️ Top 10 Scorers

sns.barplot(data=top_scorers, x="PTS", y="Player", palette="viridis")

⚽ Minutes vs. Points by Position

df_clean = df[['MP', 'PTS', 'Pos']].dropna()
df_clean['Pos'] = df_clean['Pos'].astype(str).str.strip()
sns.scatterplot(data=df_clean, x="MP", y="PTS", hue="Pos")

🎯 Correlation Heatmap

sns.heatmap(df_clean.corr(numeric_only=True), annot=True, cmap="coolwarm")

🔄 Role Comparison: Starters vs Bench

df['Role'] = df['GS'].apply(lambda x: 'Starter' if x > 30 else 'Bench')
sns.boxplot(data=df, x='Role', y='PTS')

🔀 Player Role Clustering with KMeans

🏋️ Objective

Segment players into:

High-Impact Starters

Role Players

Bench/Development

⚖️ Features Used

features = ['MP', 'PTS', 'AST', 'TRB', 'FG%', 'STL', 'BLK', 'TOV']
df_cluster = df[features].dropna()

🌍 Apply KMeans

scaler = StandardScaler()
X_scaled = scaler.fit_transform(df_cluster)
kmeans = KMeans(n_clusters=3, random_state=42)
df_cluster['Cluster'] = kmeans.fit_predict(X_scaled)

📈 Label the Clusters

label_map = {
    0: 'High-Impact Starter',
    1: 'Role Player',
    2: 'Bench/Development'
}
df_cluster['Role'] = df_cluster['Cluster'].map(label_map)

📊 Visualize Clusters

sns.scatterplot(data=df_cluster, x='MP', y='PTS', hue='Role', palette='Set2')

📅 Summary

This analysis provides a data-driven breakdown of the Golden State Warriors' player contributions using core NBA stats. Clustering helps segment players for deeper insight into roster construction, playing time decisions, and development planning.

📁 Files Included

GSW_2025_PerGame.csv – Raw data

GSW_Player_Analysis.ipynb – Jupyter Notebook with full analysis

README.md – Project overview

🌟 Tools Used

Python (Pandas, Seaborn, scikit-learn)

Jupyter Notebook

Data sourced from Basketball Reference (https://www.basketball-reference.com/teams/GSW/2025.html)
