### 1.1 Отношение (таблица)

<details>
<summary><b>Задание №1:</b> Создание таблицы.</summary>
  
```mysql
CREATE TABLE book (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50),
    author VARCHAR(30),
    price DECIMAL(8, 2),
    amount INT
    )
```
</details>

<details>
<summary><b>Задание №2:</b> Вставка записи в таблицу.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
VALUES ("Мастер и Маргарита", "Булгаков М.А.", 670.99, 3)
```
</details>

<details>
<summary><b>Задание №3:</b> Вставка нескольких записей в таблицу.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
VALUES ("Белая гвардия", "Булгаков М.А.", 540.50, 5),
       ("Идиот", "Достоевский Ф.М.", 460.00, 10),
       ("Братья Карамазовы", "Достоевский Ф.М.", 799.01, 2);
```
</details>

### 1.2 Выборка данных

<details>
<summary><b>Задание №1:</b> Выборка всех данных из таблицы.</summary>
  
```mysql
SELECT *
FROM book
```
</details>

<details>
<summary><b>Задание №2:</b> Выборка отдельных столбцов из таблицы.</summary>
  
```mysql
SELECT author, title, price
FROM book
```
</details>

<details>
<summary><b>Задание №3:</b> Присвоение новых имен столбцам при формировании выборки.</summary>
  
```mysql
SELECT title AS Название, author AS Автор
FROM book
```
</details>

<details>
<summary><b>Задание №4:</b> Выборка данных с созданием вычисляемого столбца.</summary>
  
```mysql
SELECT title, amount, amount * 1.65 AS pack
FROM book
```
</details>

<details>
<summary><b>Задание №5:</b> Выборка данных, вычисляемые столбцы, математические функции.</summary>
  
```mysql
SELECT title, author, amount, ROUND((price*0.7), 2) as new_price
FROM book
```
</details>

<details>
<summary><b>Задание №6:</b> Выборка данных, вычисляемые столбцы, логические функции.</summary>
  
```mysql
SELECT author, title, ROUND(price * IF(author = "Булгаков М.А.", 1.1, IF(author = "Есенин С.А.", 1.05, 1)), 2) AS new_price
FROM book
```
</details>

<details>
<summary><b>Задание №7:</b> Выборка данных по условию.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE amount < 10
```
</details>

<details>
<summary><b>Задание №8:</b> Выборка данных, логические операции.</summary>
  
```mysql
SELECT title, author, price, amount
FROM book
WHERE (price < 500 OR price > 600) AND price * amount >= 5000
```
</details>

<details>
<summary><b>Задание №9:</b> Выборка данных, операторы BETWEEN, IN.</summary>
  
```mysql
SELECT title, author
FROM book
WHERE (price BETWEEN 540.50 AND 800) AND amount IN (2,3,5,7)
```
</details>

<details>
<summary><b>Задание №10:</b> Выборка данных с сортировкой.</summary>
  
```mysql
SELECT author, title
FROM book
WHERE amount BETWEEN 2 AND 14
ORDER BY 1 DESC, 2 ASC
```
</details>

<details>
<summary><b>Задание №11:</b> Выборка данных, оператор LIKE.</summary>
  
```mysql
SELECT title, author
FROM book
WHERE title LIKE "_% _%" AND (author LIKE "% С._." OR  author LIKE "% _.С.")
ORDER BY 1 ASC
```
</details>

<details>
<summary><b>Задание №12:</b> Задание.</summary>
  
```mysql
SELECT title AS Название, author AS Автор
FROM book
WHERE (price BETWEEN 500 AND 600) AND amount IN (2, 3)
```
</details>

### 1.3 Запросы, групповые операции

<details>
<summary><b>Задание №1:</b> Выбор уникальных элементов столбца.</summary>
  
```mysql
SELECT amount
FROM book
GROUP BY amount
```
</details>

<details>
<summary><b>Задание №2:</b> Выборка данных, групповые функции SUM и COUNT.</summary>
  
```mysql
SELECT author AS Автор, COUNT(title) AS Различных_книг, SUM(amount) AS Количество_экземпляров
FROM book
GROUP BY 1
```
</details>
<details>
<summary><b>Задание №3:</b> Выборка данных, групповые функции MIN, MAX и AVG.</summary>
  
```mysql
SELECT author, MIN(price) AS Минимальная_цена, MAX(price) AS Максимальная_цена, AVG(price) AS Средняя_цена
FROM book
GROUP BY author
```
</details>
<details>
<summary><b>Задание №4:</b> Выборка данных c вычислением, групповые функции.</summary>
  
```mysql
SELECT author, SUM(price * amount) AS Стоимость, ROUND(SUM((price * amount * 0.18) / 1.18), 2) AS НДС, ROUND(SUM((price * amount) / 1.18), 2) AS Стоимость_без_НДС
FROM book
GROUP BY author
```
</details>
<details>
<summary><b>Задание №5:</b> Вычисления по таблице целиком.</summary>
  
```mysql
SELECT MIN(price) AS Минимальная_цена, MAX(price) AS Максимальная_цена, ROUND(AVG(price), 2) AS Средняя_цена
FROM book
```
</details>
<details>
<summary><b>Задание №6:</b> Выборка данных по условию, групповые функции.</summary>
  
```mysql
SELECT ROUND(AVG(price), 2) AS Средняя_цена, ROUND(SUM(price * amount), 2) AS Стоимость
FROM book
WHERE amount BETWEEN 5 AND 14
```
</details>
<details>
<summary><b>Задание №7:</b> Выборка данных по условию, групповые функции, WHERE и HAVING.</summary>
  
```mysql
SELECT author, SUM(price * amount) AS Стоимость
FROM book
WHERE title NOT IN ("Идиот", "Белая гвардия")
GROUP BY author
HAVING Стоимость > 5000
ORDER BY 2 DESC
```
</details>
<details>
<summary><b>Задание №8:</b> Задание.</summary>
  
```mysql
SELECT author, SUM(price * amount) AS Стоимость
FROM book
WHERE title <> "Идиот" AND title <> "Белая гвардия" AND author != "Булгаков М.А."
GROUP BY author
HAVING Стоимость > 1000
ORDER BY 2 DESC
```
</details>

### 1.4 Вложенные запросы

<details>
<summary><b>Задание №1:</b> Вложенный запрос, возвращающий одно значение.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE price <= (
    SELECT AVG(price)
    FROM book
    )
ORDER BY 3 DESC
```
</details>
<details>
<summary><b>Задание №2:</b> Использование вложенного запроса в выражении.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE ABS(price - (SELECT MIN(price) FROM book)) <= 150
ORDER BY 3 ASC
```
</details>
<details>
<summary><b>Задание №3:</b> Вложенный запрос, оператор IN.</summary>
  
```mysql
SELECT author, title, amount
FROM book
WHERE amount NOT IN (
    SELECT amount
    FROM book
    GROUP BY 1
    HAVING COUNT(*) > 1)
```
</details>
<details>
<summary><b>Задание №4:</b> Вложенный запрос, операторы ANY и ALL.</summary>
  
```mysql
SELECT author, title, price
FROM book
WHERE price < ANY (
    SELECT MIN(price)
    FROM book
    GROUP BY author
    )
```
</details>
<details>
<summary><b>Задание №5:</b> Вложенный запрос после SELECT.</summary>
  
```mysql
SELECT title, author, amount, ABS((SELECT MAX(amount) FROM book) - amount) AS Заказ
FROM book
HAVING Заказ > 0
```
</details>
<details>
<summary><b>Задание №6:</b> Задание.</summary>
  
```mysql
SELECT title, author, price, amount, ((SELECT MAX(amount) FROM book) - amount ) AS Заказ 
FROM book
WHERE price < ANY (SELECT MAX(price) FROM book)
HAVING Заказ > 5
```
</details>

### 1.5 Запросы корректировки данных
<details>
<summary><b>Задание №1:</b> Создание пустой таблицы.</summary>
  
```mysql
CREATE TABLE supply (
    supply_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50),
    author VARCHAR(30),
    price DECIMAL(8, 2),
    amount INT
    )
```
</details>
<details>
<summary><b>Задание №2:</b> Добавление записей в таблицу.</summary>
  
```mysql
INSERT INTO supply (title, author, price, amount)
VALUES ("Лирика", "Пастернак Б.Л.", 518.99, 2),
       ("Черный человек", "Есенин С.А.", 570.20, 6),
       ("Белая гвардия", "Булгаков М.А.", 540.50, 7),
       ("Идиот", "Достоевский Ф.М.", 360.80, 3)
```
</details>
<details>
<summary><b>Задание №3:</b> Добавление записей из другой таблицы.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
SELECT title, author, price, amount
FROM supply
WHERE author NOT IN ("Достоевский Ф.М.", "Булгаков М.А.")
```
</details>
<details>
<summary><b>Задание №4:</b> Добавление записей, вложенные запросы.</summary>
  
```mysql
INSERT INTO book (title, author, price, amount)
SELECT title, author, price, amount
FROM supply
WHERE author NOT IN (
    SELECT author
    FROM book
    )
```
</details>
<details>
<summary><b>Задание №5:</b> Запросы на обновление.</summary>
  
```mysql
UPDATE book
SET price = price * 0.9
WHERE amount BETWEEN 5 AND 10
```
</details>
<details>
<summary><b>Задание №6:</b> Запросы на обновление нескольких столбцов.</summary>
  
```mysql
UPDATE book
SET buy = IF(buy > amount, amount, buy),
    price = IF(buy = 0, price * 0.9, price)
```
</details>
<details>
<summary><b>Задание №7:</b> Запросы на обновление нескольких таблиц .</summary>
  
```mysql
UPDATE book, supply
SET book.amount = book.amount + supply.amount,
    book.price = (book.price + supply.price) / 2
WHERE book.title = supply.title AND book.author = supply.author
```
</details>
<details>
<summary><b>Задание №8:</b> Запросы на удаление.</summary>
  
```mysql
DELETE
FROM supply
WHERE author IN (
    SELECT author
    FROM book
    GROUP BY 1
    HAVING SUM(amount) > 10
    )
```
</details>
<details>
<summary><b>Задание №9:</b> Запросы на создание таблицы.</summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №10:</b> Создание таблицы.</summary>
  
```mysql

```
</details>

### 1.6 Запросы корректировки данных
<details>
<summary><b>Задание №2:</b> Создание таблицы.</summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №2:</b> Создание таблицы.</summary>
  
```mysql

```
</details>
<details>
<summary><b>Задание №2:</b> Создание таблицы.</summary>
  
```mysql

```
</details>
