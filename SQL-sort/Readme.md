# SQL-sort
#### 從 nba 資料庫的 career_summaries 資料表中依據 ppg（Points per game，場均得分）找出場均得分最高的 10 名球員，參考下列的預期查詢結果

```sql
SELECT personId,
       ppg
   FROM career_summaries
  ORDER BY ppg DESC
  LIMIT 10;
```

#### 從 covid19 資料庫的 time_series 資料表中依據 Daily_Cases 找出前十個單日新增確診數最多的日期，參考下列的預期查詢結果

```sql
SELECT Date,
       Country_Region,
       Daily_Cases
   FROM time_series
  ORDER BY Daily_Cases DESC
  LIMIT 10;
```

####   從 nba 資料庫的 career_summaries 資料表中依據 assists、turnovers 欄位以及下列公式衍生計算助攻失誤比，使用 CAST 函數讓衍生計算欄位的資料類型為浮點數 REAL，找出助攻失誤比最高的前 10 名球員，參考下列的預期查詢結果
Assists Turnover Ratio=assists/turnovers

```sql
SELECT personId,
       assists,
       turnovers
   FROM career_summaries
  ORDER BY CAST(assists as real)/ turnovers DESC
  LIMIT 10;
```
