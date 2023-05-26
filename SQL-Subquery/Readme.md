# SQL-Subquery
#### 從 nba 資料庫的 players 資料表運用子查詢找出 NBA 中身高最高與最矮的球員是誰，參考下列的預期查詢結果

```sql
SELECT firstName,
       lastName,
       heightMeters
  FROM players
 WHERE heightMeters = (
                          SELECT MAX(heightMeters) 
                            FROM players
                      )
OR 
       heightMeters = (
                          SELECT MIN(heightMeters) 
                            FROM players
                      );
```

#### 從 nba 資料庫的 players 資料表運用子查詢計算球員的國籍佔比，參考下列的預期查詢結果

```sql
SELECT country,
       ROUND(COUNT( * ) * 1.0 / (
                                    SELECT COUNT( * ) 
                                      FROM players
                                ), 6) AS player_percentage
  FROM players
 GROUP BY country
 ORDER BY COUNT( * ) DESC;
```

####   從 nba 資料庫運用子查詢找出 NBA 的場均得分王（ppg），參考下列的預期查詢結果

```sql
SELECT firstName,
       lastName
  FROM players
 WHERE personId = (
                      SELECT personId
                        FROM career_summaries
                       WHERE ppg = (
                                       SELECT MAX(ppg) 
                                         FROM career_summaries
                                   )
                  );
```


####   從 nba 資料庫運用子查詢找出目前布魯克林籃網隊（Brooklyn Nets）的球員名單，參考下列的預期查詢結果

```sql
SELECT firstName,
       lastName
  FROM players
 WHERE teamId = (
                    SELECT teamId
                      FROM teams
                     WHERE fullName = 'Brooklyn Nets'
                );
```


####   從 twElection2020 資料庫的 presidential 資料表計算各組候選人的得票率，參考下列的預期查詢結果

```sql
SELECT candidate_id,
       ROUND(SUM(votes) * 100.0 / (
                                      SELECT SUM(votes) 
                                        FROM presidential
                                  ), 2) || '%' AS votes_percentage
  FROM presidential
 GROUP BY candidate_id;
```
