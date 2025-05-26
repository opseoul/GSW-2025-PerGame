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
