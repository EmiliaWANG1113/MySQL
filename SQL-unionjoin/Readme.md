# SQL-unionjoin
#### 從 covid19 資料庫查詢截至 2021-03-31 全球前十大確診人數的國家，參考下列的預期查詢結果

```sql
SELECT lookup_table.Country_Region,
       SUM(daily_report.Confirmed) AS total_confirmed 
FROM lookup_table
JOIN daily_report
ON lookup_table.Combined_Key=daily_report.Combined_Key
GROUP BY Country_Region
ORDER BY total_confirmed DESC
LIMIT 10;
```

#### 從 twElection2020 資料庫查詢中國國民黨、民主進步黨與親民黨在不分區立委與區域立委的得票率，參考下列的預期查詢結果

```sql
SELECT parties.party,
       '不分區立委'  as election,     
       ROUND(SUM(legislative_at_large.votes) *1.0 /(SELECT SUM(legislative_at_large.votes)
FROM legislative_at_large),4) as votes_percentage
FROM legislative_at_large
JOIN parties
ON legislative_at_large.party_id=parties.id
WHERE parties.party IN('中國國民黨','民主進步黨','親民黨')
GROUP BY parties.party
UNION
SELECT parties.party,
      '區域立委'  as election,
      ROUND(SUM(legislative_regional.votes) *1.0 /(SELECT SUM(legislative_regional.votes)
FROM legislative_regional),4) as votes_percentage
FROM legislative_regional
JOIN candidates
ON legislative_regional.candidate_id=candidates.id
JOIN parties
ON candidates.party_id=parties.id
WHERE parties.party IN('中國國民黨','民主進步黨','親民黨')
GROUP BY parties.party
ORDER BY election;
```

####   從 nba 資料庫查詢截至 2021-03-31 洛杉磯湖人隊（Los Angeles Lakers）球員的生涯場均得分 ppg，參考下列的預期查詢結果

```sql
SELECT teams.fullName as team_name,
       players.firstName || ' ' || players.lastName as player_name,career_summaries.ppg
FROM teams
JOIN players
ON teams.teamId=players.teamId
JOIN career_summaries
ON players.personId=career_summaries.personId
WHERE teams.fullName = 'Los Angeles Lakers'
ORDER BY ppg DESC;
```


####   從 nba 資料庫查詢各個球隊的得分王（生涯場均得分 ppg 全隊最高）是誰，將查詢結果依隊伍名排序，參考下列的預期查詢結果

```sql
SELECT teams.fullName as team,
       players.firstName || ' ' || players.lastName as player,MAX(career_summaries.ppg) as ppg
FROM teams
JOIN players
ON teams.teamId=players.teamId
JOIN career_summaries
ON players.personId=career_summaries.personId
GROUP BY team;
```


####   從 imdb 資料庫中查詢 Tom Hanks 與 Leonardo DiCaprio 在 IMDb.com 最高評價的 250 部電影中演出哪些電影，依據 casting 資料表中的 ord 衍生計算欄位 is_lead_actor 註記是否為第一主角（ord 若為 1 表示為第一主角），將查詢結果依 release_year 排序，參考下列的預期查詢結果

```sql
SELECT movies.release_year,
       movies.title,
       actors.name,
       casting.ord==1 as is_lead_actor 
FROM movies
JOIN casting
ON movies.id = casting.movie_id
JOIN actors
ON casting.actor_id = actors.id
WHERE actors.name IN ('Tom Hanks','Leonardo DiCaprio')
ORDER BY movies.release_year;
```
