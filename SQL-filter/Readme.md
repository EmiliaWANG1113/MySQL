# SQL-filter
#### 從 covid19 資料庫的 time_series 資料表將台灣的觀測值篩選出來，參考下列的預期查詢結果

```sql
SELECT Country_Region,
       Date,
       Confirmed,
       Daily_Cases
   FROM time_series
  WHERE Country_Region='Taiwan';
```

#### 從 imdb 資料庫的 movies 資料表將上映年份為 1994 的電影篩選出來，參考下列的預期查詢結果

```sql
SELECT title,
       rating,
       director,
       runtime
   FROM movies
  WHERE release_year=1994;
```

####   從 imdb 資料庫的 actors 資料表將 Tom Hanks、Christian Bale、Leonardo DiCaprio 篩選出來，參考下列的預期查詢結果

```sql
SELECT id,
       name
   FROM actors
  WHERE name IN('Tom Hanks','Christian Bale','Leonardo DiCaprio');
```

####    從 imdb 資料庫的 movies 資料表篩選出由 Christopher Nolan 或 Peter Jackson 所導演的電影，參考下列的預期查詢結果

```sql
SELECT title,
       director
   FROM movies
  WHERE director IN('Christopher Nolan','Peter Jackson');
```

####    從 covid19 資料庫的 lookup_table 資料表篩選出 Country_Region 名稱有 land 的國家，參考下列的預期查詢結果

```sql
SELECT DISTINCT(Country_Region)
   FROM lookup_table
  WHERE Country_Region LIKE '%land%';
```
