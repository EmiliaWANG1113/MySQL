# SQL-practice
#### 從 covid19 資料庫查詢兩艘郵輪（Grand Princess 與 Diamond Princess）的資訊，參考下列的預期查詢結果

```sql
SELECT lookup_table.iso2,
       lookup_table.Country_Region,
       lookup_table.Province_State,
       daily_report.Confirmed
FROM daily_report
JOIN lookup_table
ON daily_report.Combined_Key =lookup_table.Combined_Key
WHERE lookup_table.Province_State IN('Grand Princess','Diamond Princess');
```


#### 從 covid19 資料庫查詢截至 2021-03-31 所有國家確診與死亡人數的資訊，參考下列的預期查詢結果

```sql
SELECT lookup_table.Country_Region,
       SUM(daily_report.Confirmed) as Confirmed,
       SUM(daily_report.Deaths) as Deaths
FROM daily_report
JOIN lookup_table
ON daily_report.Combined_Key =lookup_table.Combined_Key
GROUP BY lookup_table.Country_Region;
```



####  從 imdb 資料庫查詢「魔戒三部曲」與「蝙蝠俠三部曲」的電影資訊與演員名單，三部曲電影系列中演員重複出演的情況是正常的，這時顯示獨一值即可，參考下列的預期查詢結果

```sql
SELECT CASE WHEN movies.title LIKE '%Lord of the Rings%' THEN 'The Lord of the Rings Trilogy' 
       ELSE  'Batman Trilogy' END AS trilogy,
       actors.name
FROM movies
JOIN casting
ON movies.id = casting.movie_id
JOIN actors
ON casting.actor_id = actors.id
WHERE movies.title LIKE '%Lord of the Rings%' OR
      movies.title LIKE '%Batman%' OR
      movies.title LIKE '%Dark Knight%'
GROUP BY trilogy,
         name;
```


####   從 nba 資料庫查詢截至 2021-03-31 的得分王（生涯場均得分 ppg 最高）、助攻王（生涯場均助攻 apg 最高）、籃板王（生涯場均籃板 rpg 最高）、抄截王（生涯場均抄截 spg 最高）以及阻攻王（生涯場均阻攻 bpg 最高），參考下列的預期查詢結果

```sql
SELECT players.firstname,
       players.lastname,
       'ppg' as category,
       career_summaries.ppg as value
FROM career_summaries
JOIN players
ON  career_summaries.personId = players.personId
WHERE ppg=(SELECT MAX(ppg) 
FROM career_summaries) 
UNION
SELECT players.firstname,
       players.lastname,
       'apg' as category,
       career_summaries.apg as value
FROM career_summaries
JOIN players
ON  career_summaries.personId = players.personId
WHERE apg=(SELECT MAX(apg) 
FROM career_summaries) 
UNION
SELECT players.firstname,
       players.lastname,
       'rpg' as category,
       career_summaries.rpg as value
FROM career_summaries
JOIN players
ON  career_summaries.personId = players.personId
WHERE rpg=(SELECT MAX(rpg) 
FROM career_summaries)
UNION
SELECT players.firstname,
       players.lastname,
       'spg' as category,
       career_summaries.spg as value
FROM career_summaries
JOIN players
ON  career_summaries.personId = players.personId
WHERE spg=(SELECT MAX(spg) 
FROM career_summaries) 
UNION
SELECT players.firstname,
       players.lastname,
       'bpg' as category,
       career_summaries.bpg as value
FROM career_summaries
JOIN players
ON  career_summaries.personId = players.personId
WHERE bpg=(SELECT MAX(bpg) 
FROM career_summaries) 
;
```


####  從 twElection2020 資料庫查詢三組總統候選人在各縣市的得票數，參考下列的預期查詢結果
```sql
SELECT soong_yu.county,
       soong_yu.soong_yu_votes,
       han_chang.han_chang_votes,
       tsai_lai.tsai_lai_votes
FROM (SELECT admin_regions.county,
       SUM(presidential.votes) as soong_yu_votes
FROM presidential
JOIN admin_regions
ON presidential.admin_region_id=admin_regions.id
WHERE presidential.candidate_id=1
GROUP BY admin_regions.county) as soong_yu
JOIN (SELECT admin_regions.county,
       SUM(presidential.votes) as han_chang_votes
FROM presidential
JOIN admin_regions
ON presidential.admin_region_id=admin_regions.id
WHERE presidential.candidate_id=2
GROUP BY admin_regions.county) as han_chang
ON soong_yu.county=han_chang.county
JOIN (SELECT admin_regions.county,
       SUM(presidential.votes) as tsai_lai_votes
FROM presidential
JOIN admin_regions
ON presidential.admin_region_id=admin_regions.id
WHERE presidential.candidate_id=3
GROUP BY admin_regions.county) as tsai_lai
ON soong_yu.county=tsai_lai.county;
```


####  從 covid19 資料庫查詢截至 2021-03-31 美國前十大確診人數的州別，參考下列的預期查詢結果
```sql
SELECT lookup_table.Province_State,
       SUM(Confirmed) as Confirmed
FROM daily_report
JOIN lookup_table
ON daily_report.Combined_Key=lookup_table.Combined_Key
WHERE lookup_table.Country_Region='US'
GROUP BY lookup_table.Province_State
ORDER BY Confirmed DESC
LIMIT 10;
```


####  從 covid19 資料庫查詢截至 2021-03-31 台灣、日本、中國、南韓與新加坡五個國家的確診與死亡人數的資訊，參考下列的預期查詢結果
```sql
SELECT lookup_table.Country_Region,
       SUM(Confirmed) as Confirmed,
       SUM(Deaths) as Deaths
FROM daily_report
JOIN lookup_table
ON daily_report.Combined_Key=lookup_table.Combined_Key
WHERE lookup_table.Country_Region IN ('China','Japan','Korea, South','Singapore','Taiwan')
GROUP BY lookup_table.Country_Region;
```


####  從 imdb 資料庫查詢出現最多次的導演為誰，參考下列的預期查詢結果
```sql
SELECT director,
       counts
FROM (SELECT director,
       COUNT(director) as counts
FROM movies
GROUP BY director) as counts_by_director
WHERE counts=(SELECT MAX(counts)
FROM(SELECT director,
       COUNT(director) as counts
FROM movies
GROUP BY director) as counts_by_director);
```


####  從 imdb 資料庫查詢出現最多次的演員為誰，參考下列的預期查詢結果
```sql
SELECT actor_id,name,counts
FROM(SELECT casting.actor_id as actor_id,
       name,
       COUNT(actor_id) as counts
FROM actors
JOIN casting
ON actors.id=casting.actor_id
GROUP BY actor_id
)
WHERE counts=(SELECT MAX(counts)
FROM (SELECT casting.actor_id as actor_id,
       name,
       COUNT(actor_id) as counts
FROM actors
JOIN casting
ON actors.id=casting.actor_id
GROUP BY actor_id));
```


####  從 imdb 資料庫查詢評等大於等於 8.8（rating >= 8.8）電影的導演以及第一主角（ord = 1），參考下列的預期查詢結果
```sql
SELECT title,director,actors.name as lead_actor
FROM movies
JOIN casting
ON movies.id=casting.movie_id
JOIN actors
ON casting.actor_id=actors.id
WHERE movies.rating >= 8.8 and casting.ord=1;
```


####  從 nba 資料庫查詢截至 2021-03-31 的得分王（生涯總得分 points 最高）、助攻王（生涯總助攻 assists 最高）、籃板王（生涯總籃板 totReb 最高）、抄截王（生涯總抄截 steals 最高）以及阻攻王（生涯總阻攻 blocks 最高），參考下列的預期查詢結果
```sql
SELECT players.firstName,
       players.lastName,
       'points' as category,
        career_summaries.points AS value 
FROM players
JOIN career_summaries
ON players.personId = career_summaries.personId
WHERE career_summaries.personId=(SELECT personId
FROM career_summaries
WHERE points=(SELECT MAX(points)
FROM career_summaries))
UNION 

SELECT players.firstName,
       players.lastName,
       'assists' as category,
        career_summaries.assists AS value 
FROM players
JOIN career_summaries
ON players.personId = career_summaries.personId
WHERE career_summaries.personId=(SELECT personId
FROM career_summaries
WHERE assists=(SELECT MAX(assists)
FROM career_summaries))

UNION 

SELECT players.firstName,
       players.lastName,
       'totReb' as category,
        career_summaries.totReb AS value 
FROM players
JOIN career_summaries
ON players.personId = career_summaries.personId
WHERE career_summaries.personId=(SELECT personId
FROM career_summaries
WHERE totReb=(SELECT MAX(totReb)
FROM career_summaries))

UNION 

SELECT players.firstName,
       players.lastName,
       'steals' as category,
        career_summaries.steals AS value 
FROM players
JOIN career_summaries
ON players.personId = career_summaries.personId
WHERE career_summaries.personId=(SELECT personId
FROM career_summaries
WHERE steals=(SELECT MAX(steals)
FROM career_summaries))

UNION 

SELECT players.firstName,
       players.lastName,
       'blocks' as category,
        career_summaries.blocks AS value 
FROM players
JOIN career_summaries
ON players.personId = career_summaries.personId
WHERE career_summaries.personId=(SELECT personId
FROM career_summaries
WHERE blocks=(SELECT MAX(blocks)
FROM career_summaries));
```


####  從 nba 資料庫查詢截至 2021-03-31 各球隊陣中場均得分大於等於 20 分（ppg >= 20）的球員人數，參考下列的預期查詢結果
```sql
SELECT teams.fullName as team_name,
       IFNULL(top_scores_by_teams.number_of_players,0) as number_of_players
FROM teams
LEFT JOIN(SELECT teams.fullName,
                 COUNT(*) as number_of_players
            FROM career_summaries
            JOIN players
            ON career_summaries.personId=players.personId
            JOIN teams
            ON players.teamId=teams.teamId
            WHERE career_summaries.ppg >= 20
            GROUP BY teams.fullName) AS top_scores_by_teams
        ON teams.fullName=top_scores_by_teams.fullName
ORDER BY number_of_players DESC,team_name;
```

####  從 twElection2020 資料庫查詢中國國民黨與民主進步黨在 2020 年選舉的得票率，包含總統副總統、不分區立委與區域立委，參考下列的預期查詢結果
```sql
SELECT presidential_result.party,
       presidential_result.presidential,
       legislative_regional_result.legislative_regional,
       legislative_at_large.legislative_at_large
FROM (SELECT CASE WHEN candidate_id=2 THEN '中國國民黨'
             ELSE '民主進步黨' END as party,
             ROUND(CAST(SUM(votes) as real) *100/ (SELECT SUM(votes) FROM presidential),2) || '%' as presidential
      FROM presidential
      WHERE candidate_id IN(2,3)
      GROUP BY candidate_id) as presidential_result
JOIN (SELECT parties.party,
             ROUND(CAST(SUM(votes) as real) *100/ (SELECT SUM(votes) FROM legislative_regional),2) || '%' as legislative_regional
      FROM legislative_regional
      JOIN candidates
      ON legislative_regional.candidate_id=candidates.id
      JOIN parties
      ON  candidates.party_id=parties.id
      WHERE parties.party IN('中國國民黨','民主進步黨')
      GROUP BY parties.party) as legislative_regional_result
ON presidential_result.party=legislative_regional_result.party
JOIN (SELECT parties.party,
       ROUND(CAST(SUM(votes) as real) *100/ (SELECT SUM(votes) FROM legislative_at_large),2) || '%' as legislative_at_large
      FROM legislative_at_large
      JOIN parties
      ON  legislative_at_large.party_id=parties.id
      WHERE parties.party IN('中國國民黨','民主進步黨')
      GROUP BY parties.party) as legislative_at_large
ON presidential_result.party = legislative_at_large.party;
```

####  從 twElection2020 資料庫查詢代表中國國民黨參選總統副總統的韓國瑜/張善政組合，在台灣 7,737 個選舉區（以村鄰里為一個選舉區）贏得的選舉區（得票數大於 > 蔡英文/賴清德組合）以及淨贏得票數，參考下列的預期查詢結果
```sql
SELECT admin_regions.county,
       admin_regions.town,
       admin_regions.village,
       han_chang.han_chang_votes-tsai_lai.tsai_lai_votes as net_winning_votes
FROM(SELECT admin_regions.id,
            SUM(presidential.votes) as han_chang_votes
     FROM presidential
     JOIN admin_regions
     ON presidential.admin_region_id = admin_regions.id
     WHERE presidential.candidate_id=2
     GROUP BY admin_regions.id) as han_chang
JOIN(SELECT admin_regions.id,
            SUM(presidential.votes) as tsai_lai_votes
     FROM presidential
     JOIN admin_regions
     ON presidential.admin_region_id = admin_regions.id
     WHERE presidential.candidate_id=3
     GROUP BY admin_regions.id) as tsai_lai
ON han_chang.id=tsai_lai.id
JOIN admin_regions
ON han_chang.id = admin_regions.id
WHERE net_winning_votes>0
ORDER BY net_winning_votes DESC;
```
