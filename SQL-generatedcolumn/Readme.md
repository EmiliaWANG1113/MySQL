# SQL-generatedcolumn
#### 從 covid19 資料庫的 daily_report 資料表根據 Confirmed、Recovered、Deaths 欄位以及下列公式衍生計算欄位 Active，參考下列的預期查詢結果
Active=Confirmed−Recovered−Deaths

```sql
SELECT Confirmed,
       Deaths,
       Recovered,
       Confirmed-Deaths-Recovered  AS  Active
  FROM daily_report;
```

#### 從 nba 資料庫的 players 資料表依據 heightMeters、weightKilograms 欄位以及下列公式衍生計算欄位 bmi，參考下列的預期查詢結果

```sql
SELECT heightMeters,
       weightKilograms,
       weightKilograms/(heightMeters*heightMeters) AS  bmi
  FROM players;
```

####  從 nba 資料庫的 teams 資料表連接 confName、divName 欄位後使用 DISTINCT 去除重複值，參考下列的預期查詢結果
```sql
SELECT DISTINCT confName||', '||divName as conf_div
  FROM teams;
```



