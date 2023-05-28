# SQL-SELECT
#### 從 twElection2020 資料庫的 admin_regions 資料表選擇所有變數，並且使用 LIMIT 5 顯示前五列資料，參考下列的預期查詢結果
```sql
SELECT * 
    FROM admin_regions
LIMIT 5;
```

#### 從 nba 資料庫的球隊資料表 teams 中選擇 confName、divName、fullName 三個變數，並且使用 LIMIT 10 顯示前十列資料，參考下列預期的查詢結果
```sql
SELECT confName,
        divName,
        fullName 
    FROM teams
LIMIT 10;
```

#### 從 nba 資料庫的球員資料表 players 中選擇 firstName、lastName 兩個變數，並依序取別名為 first_name、last_name，使用 LIMIT 5 顯示前五列資料，參考下列預期的查詢結果
```sql
SELECT firstName as first_name,
        lastName as last_name 
    FROM players
LIMIT 5;
```

#### 從 twElection2020 資料庫的 admin_regions 資料表選擇「不重複」的縣市（county），參考下列的預期查詢結果
```sql
SELECT DISTINCT  county as distinct_counties
    FROM admin_regions;
```

#### 從 nba 資料庫的 teams 資料表選擇「不重複」的分組（divName），參考下列的預期查詢結果
```sql
SELECT DISTINCT  divName as distinct_divisions
    FROM teams;
```
