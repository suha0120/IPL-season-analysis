# IPL-season-analysis
# 🏏 IPL Analysis Dashboard (2008–2025) - Power BI Project  

## 📌 Project Overview  
This project is an **interactive Power BI Dashboard** that analyzes the Indian Premier League (IPL) seasons from **2008 to 2025**.  
It helps users explore season-wise insights like:  
- ✅ Total fours & sixes  
- ✅ Orange Cap (highest run-scorer)  
- ✅ Purple Cap (highest wicket-taker)  
- ✅ Season winner & runner-up  
- ✅ Team and player performance  

The dashboard is built using **Power BI** with data modeling, DAX queries, and interactive visuals.  

---

## 🔁 Workflow  

### 1️⃣ Data Collection  
- IPL datasets (2008–2025) from sources like Kaggle.  
- Data files:  
  - `ipl_matches_data` (match details)  
  - `ball_by_ball_data` (ball-level events)  
  - `players_data_updated` (players with photos)  
  - `teams_data` (team names & logos)  

### 2️⃣ Data Cleaning & Transformation (Power Query)  
- Removed null/duplicate rows  
- Standardized team & player names  
- Corrected data types (date, text, numbers)  
- Ensured consistency across tables  

### 3️⃣ Data Modeling  
- Relationships between tables using keys:  
  - `match_id` → matches vs ball-by-ball  
  - `player_name` → players vs ball data  
  - `team_name` → matches vs teams  

### 4️⃣ DAX Measures  
Some important **DAX queries** used:  
 
```DAX
Total Fours = COUNTROWS(FILTER(ball_by_ball_data, ball_by_ball_data[batter_runs] = 4))

Total Sixes = COUNTROWS(FILTER(ball_by_ball_data, ball_by_ball_data[batter_runs] = 6))

Orange Cap = TOPN(1, SUMMARIZE(ball_by_ball_data, players_data_updated[player_name],
"Runs", SUM(ball_by_ball_data[batter_runs])), [Runs], DESC)

Purple Cap = TOPN(1, SUMMARIZE(ball_by_ball_data, players_data_updated[player_name],
"Wickets", COUNT(ball_by_ball_data[is_wicket])), [Wickets], DESC)


Season Winner =
VAR SelectedSeason = SELECTEDVALUE(ipl_matches_data[season])
VAR FinalMatchDate =
    CALCULATE(MAX(ipl_matches_data[match_date]), ipl_matches_data[season] = SelectedSeason)
VAR FinalMatchWinner =
    CALCULATE(MAX(ipl_matches_data[match_winner]),
              ipl_matches_data[season] = SelectedSeason,
              ipl_matches_data[match_date] = FinalMatchDate)
RETURN FinalMatchWinner

```

### 5️⃣ Dashboard Design

Interactive visuals: bar charts, tables, KPIs, and slicers

Dynamic filters: by Season, Player, Team

Logos & player images: via LOOKUPVALUE for a better UI

Color theme: IPL-inspired

### 📊 Key Insights 

📌 Season-wise winner & runner-up  

📌 Top batsman (Orange Cap) and bowler (Purple Cap)  

📌 Team-wise and player-wise statistics  

📌 Trend of fours & sixes across years  
