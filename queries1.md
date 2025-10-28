1. Получить страны и количество пользователей
```sql
SELECT country, COUNT(*) AS users_count
FROM "user"
GROUP BY country;
```
2. Средняя цена подписок
```sql
SELECT AVG(price) AS avg_price
FROM subscription;
```
3. Средняя длина треков по жанрам
```sql
SELECT genre_id, AVG(duration_seconds) AS avg_duration
FROM track
GROUP BY genre_id;
```
4. Количество альбомов по артистам
```sql
SELECT artist_id, COUNT(*) AS albums_count
FROM album
GROUP BY artist_id;
```
5. Количество треков по артистам и жанрам с использованием GROUPING SETS
```sql
SELECT artist_id, genre_id, COUNT(*) AS track_count
FROM track
GROUP BY GROUPING SETS ((artist_id, genre_id), (artist_id), (genre_id), ());
```
6. Средняя длина треков с разными уровнями агрегации (ROLLUP)
```sql
SELECT genre_id, artist_id, AVG(duration_seconds) AS avg_duration
FROM track
GROUP BY ROLLUP (genre_id, artist_id);
```
7. Список треков жанра "Rock" длительностью больше 3 минут
```sql
SELECT t.title, t.duration_seconds, g.name AS genre
FROM track t
JOIN genre g ON t.genre_id = g.id
WHERE g.name = 'Rock' AND t.duration_seconds > 180
ORDER BY t.duration_seconds DESC;
```
8. Пользователи с активной подпиской, отсортированные по дате регистрации
```sql
SELECT u.username, s.name AS subscription, u.date_joined
FROM "user" u
JOIN subscription s ON u.subscription_id = s.id
WHERE s.price > 0
ORDER BY u.date_joined ASC;
```