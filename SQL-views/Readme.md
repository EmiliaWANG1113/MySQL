# SQL-views
#### 從 covid19 資料庫建立一個虛擬資料表名為 total_confirmed_by_country_region 記錄截至 2021-03-31 全球各國的確診人數，參考下列的預期輸出

```sql
CREATE VIEW covid19.total_confirmed_by_country_region AS 
SELECT lookup_table.Country_Region,
       SUM(daily_report.Confirmed) as total_confirmed
  FROM lookup_table
  JOIN daily_report
  ON lookup_table.Combined_Key=daily_report.Combined_Key
  GROUP BY lookup_table.Country_Region;
```

####  從 twElection2020 資料庫建立一個虛擬資料表名為 presidential_total_votes 記錄三組候選人的總得票數，參考下列的預期輸出

```sql
CREATE VIEW  twElection2020.presidential_total_votes 
AS
SELECT candidates.number,
       candidates.candidate,
       SUM(presidential.votes) as total_votes
FROM candidates
JOIN presidential
ON candidates.id=presidential.candidate_id
GROUP BY number;
```

####   從 nba 資料庫建立一個虛擬資料表名為 ppg_leader_by_teams 紀錄各個球隊的得分王（生涯場均得分 ppg 全隊最高）是誰，參考下列的預期輸出

```sql
CREATE VIEW ppg_leader_by_teams
AS
SELECT teams.fullName as team,
       players.firstName,
       players.lastName,
       MAX(career_summaries.ppg) as ppg
FROM teams
JOIN players
ON teams.teamId = players.teamId
JOIN career_summaries
ON players.personId=career_summaries.personId
GROUP BY team;
```
