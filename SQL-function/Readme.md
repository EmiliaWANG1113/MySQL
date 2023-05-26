# SQL-function
#### 從 nba 資料庫的 players 資料表依據 heightMeters、weightKilograms 以及下列公式衍生計算欄位 bmi，並使用 ROUND 函數將 bmi 的小數點位數調整為 2 位，參考下列的預期查詢結果
𝐵𝑀𝐼= 𝑤𝑒𝑖𝑔ℎ𝑡/(ℎ𝑒𝑖𝑔ℎ𝑡*ℎ𝑒𝑖𝑔ℎ𝑡)

```sql
SELECT heightMeters,
       weightKilograms,
       ROUND(weightKilograms/(heightMeters*heightMeters),2) as bmi
  FROM players;
```

#### 從 nba 資料庫的 career_summaries 資料表中依據 assists、turnovers 欄位以及下列公式衍生計算助攻失誤比，使用 CAST 函數讓衍生計算欄位的資料類型為浮點數 REAL，參考下列的預期查詢結果
Assist Turnover Ratio=𝐴𝑠𝑠𝑖𝑠𝑡𝑠/𝑇𝑢𝑟𝑛𝑜𝑣𝑒𝑟𝑠

```sql
SELECT assists,
       turnovers,
       assists * 1.0 /turnovers as assist_turnover_ratio
  FROM career_summaries;
```

####  從 covid19 資料庫的 time_series 資料表依據 Date 變數，使用 STRFTIME 函數查詢時間序列資料有哪些不重複的月份，參考下列的預期查詢結果

```sql
SELECT Distinct  STRFTIME('%Y-%m',DATE) as distinct_year_month
  FROM time_series;
```


####   從 twElection2020 資料庫的 presidential 資料表利用聚合函數彙總有多少人參與了總統副總統的投票選舉，參考下列的預期查詢結果

```sql
SELECT SUM(votes) as total_presidential_votes
  FROM presidential;
```


####  從 covid19 資料庫的 daily_report 資料表利用聚合函數彙總截至 2021-03-31 全世界總確診數、總痊癒數以及總死亡數，參考下列的預期查詢結果

```sql
SELECT SUM(confirmed) as total_confirmed,
       SUM(recovered) as total_recovered,
       SUM(deaths) as total_deaths
  FROM daily_report;
```
