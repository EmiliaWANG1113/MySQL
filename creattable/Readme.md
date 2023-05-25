# SQL-creattable
#### 在已經建立且連線好的 test 資料庫新增一個資料表名為 favorite_players，具有三個欄位 name、years_pro、ppg，資料類型分別是文字（TEXT）、整數（INTEGER）與浮點數

```sql
CREATE TABLE favorite_players(
name TEXT,
years_pro INTEGER,
ppg REAL
);
```

#### 承接上題，在 test 資料庫的 favorite_players 資料表中新增五筆觀測值，參考下列的預期輸出

```sql
INSERT INTO favorite_players(name,years_pro,ppg)
VALUES
('Steve Nash',19,14.3),
('Michael Jordan',14,30.1),
('Paul Pierce',19,19.7),
('Kevin Garnett',21,17.8),
('Hakeem Olajuwon',18,21.8);
```

####   承接上題，在 test 資料庫的 favorite_players 資料表將第五位球員 Hakeem Olajuwon 替換成 Tim Duncan，參考下列的預期輸出

```sql
UPDATE favorite_players
SET   name='Tim Duncan',
      years_pro=19,
      ppg=19.0
WHERE name='Hakeem Olajuwon';
```
