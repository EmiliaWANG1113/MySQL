# SQL-condition
#### 從 covid19 資料庫的 daily_report 資料表將「美國」與「非美國」的觀測值用衍生計算欄位區分，美國的觀測值給予整數 1、非美國的觀測值給予整數 0，參考下列的預期查詢結果

```sql
SELECT Combined_Key,
       Combined_Key LIKE '%, US' as is_us
   FROM daily_report
  ORDER BY is_us;
```

#### 從 imdb 資料庫的 movies 資料表將評等超過 8.7（>8.7）的電影分類為 'Awesome'、將評等超過 8.4（>8.4）的電影分類為 'Terrific'，再將其餘的電影分類為 'Great'，參考下列的預期查詢結果

```sql
SELECT title,
       rating,
   CASE WHEN rating > 8.7 THEN 'Awesome'
        WHEN rating > 8.4 THEN 'Terrific'
        ELSE 'Great' END AS rating_category
   FROM movies;
```

####   從 twElection2020 資料庫的 admin_regions 資料表將 county 分類為 '六都'與'非六都'，參考下列的預期查詢結果

```sql
SELECT DISTINCT county,
   CASE WHEN county IN('臺北市','新北市','桃園市','臺中市','臺南市','高雄市') THEN '六都'
   ELSE '非六都' END AS county_type
   FROM admin_regions
   ORDER BY county_type;
```
