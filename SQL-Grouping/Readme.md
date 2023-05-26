# SQL-Grouping
#### 從 imdb 資料庫的 movies 資料表計算每一年有幾部在 IMDb.com 獲得高評等的經典電影，參考下列的預期查詢結果

```sql
SELECT release_year,
      COUNT(*) as number_of_movies
   FROM movies
GROUP BY release_year;
```

#### 從 imdb 資料庫的 movies 資料表計算每一年有幾部在 IMDb.com 獲得高評等的經典電影，只顯示電影數在 5 部以上（>= 5）的年份，參考下列的預期查詢結果

```sql
SELECT release_year,
      COUNT(*) as number_of_movies  
   FROM movies
GROUP BY release_year
HAVING number_of_movies>=5;
```

####   從 twElection2020 資料庫的 presidential 資料表暸解台灣 2020 總統副總統的選舉結果，參考下列的預期查詢結果

```sql
SELECT candidate_id,
    SUM(votes) as total_votes 
   FROM presidential
 GROUP BY candidate_id;
```

####   從 nba 資料庫的 players 資料表根據 country 暸解截至 2021-03-31，NBA 由哪些國家的球員所組成，參考下列的預期查詢結果

```sql
SELECT country,
    COUNT(*) as number_of_players 
   FROM players
 GROUP BY country
 ORDER BY number_of_players DESC;
```

####   從 nba 資料庫的 players 資料表根據 country 暸解截至 2021-03-31，NBA 由哪些國家的球員所組成，只顯示球員數在 2 位以上（>= 2）並在 9 位以下（<=9）的國家，參考下列的預期查詢結果

```sql
SELECT country,
    COUNT(*) as number_of_players 
   FROM players
 GROUP BY country
  HAVING number_of_players BETWEEN 2 and 9
 ORDER BY number_of_players DESC;
```

