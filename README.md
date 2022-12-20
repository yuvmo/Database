Проект "Магазин настольных игр"
=======
Выполнили: 
- Морозова Ю.
- Колесник Е.

Схема БД
------

![](https://user-images.githubusercontent.com/120600282/208681656-e8ea2b67-2106-4bd3-89cc-aa6c23a07e29.png)

Ограничения
---

Game

- id_game: PRIMARY KEY, CHECK (id > 0)
- id_publisher: PRIMARY KEY, FOREIGN KEY (id_publisher) REFERENCES Publisher(id_publisher), CHECK (id_publisher> 0)
- id_game_genre: PRIMARY KEY, FOREIGN KEY (id_game_genre) REFERENCES Game_genre(id_game_genre), CHECK (id_game_genre> 0)
- id_age_restriction: PRIMARY KEY, FOREIGN KEY (id_age_restriction) REFERENCES Age_restriction(id_age_restriction), CHECK (id_age_restriction> 0)
- id_game_status: PRIMARY KEY, FOREIGN KEY (id_game_status) REFERENCES Game_status(id_game_status), CHECK (id_game_status> 0)
name: NOT NULL
- playernum: NOT NULL
- price: NOT NULL
- amount:

Publisher

- id_publisher: PRIMARY KEY, CHECK (id_publisher>0)
- name: NOT NULL

Employee

- id_employee: PRIMARY KEY, CHECK (id_employee>0)
- id_shop: PRIMARY KEY, FOREIGN KEY (id_shop) REFERENCES Shop (id_shop), CHECK (id_shop> 0)
- fio: NOT NULL
- phonenum: NOT NULL

Shop

- id_shop: PRIMARY KEY, CHECK (id>0)
- city: NOT NULL
- address: NOT NULL

Buyer

- id_buyer: PRIMARY KEY, CHECK (id>0)
- bname: NOT NULL
- phonenum: NOT NULL
- registration: NOT NULL

Orders

- id_orders: PRIMARY KEY, CHECK (id_order > 0)
- id_buyer: PRIMARY KEY, FOREIGN KEY (id_buyer) REFERENCES Buyer(id_buyer), CHECK (id_buyer> 0)
- id_order_status: PRIMARY KEY, FOREIGN KEY (id_order_status) REFERENCES Order_status(id_order_status), CHECK (id_order_status> 0)
- id_game: PRIMARY KEY, FOREIGN KEY (id_game) REFERENCES Game(id_game), CHECK (id_game> 0)
- id_employee: PRIMARY KEY, FOREIGN KEY (id_employee) REFERENCE Employee(id_employee), CHECK (id_employee> 0)
- orders_date: NOT NULL

Order_status

- id_order_status: PRIMARY KEY, CHECK (id_order > 0)
- status: NOT NULL

Game_status

- id_game_status: PRIMARY KEY, CHECK (id_order > 0)
- gamestatus: NOT NULL

Game_genre

- id_game_genre: PRIMARY KEY, CHECK (id_order > 0)
- genre: NOT NULL

Age_restriction

- id_age_restriction: PRIMARY KEY, CHECK (id_order > 0)
- age: NOT NULL


Сущности и поля
---

***Магазин(Shop)***: сильная сущность, от которой зависит слабая сущность ***Сотрудник (Employee)***. Данная сущность хранит данные о магазине. Имеет следующие атрибуты:
- id_shop(integer) - простой, однозначный атрибут, содержащий идентификатор магазина, является первичным ключом;
- city(varchar(40)) - простой однозначный атрибут, содержащий город, где находится магазин;
- address(varchar(150)) - простой однозначный атрибут, содержащий адрес магазина;

***Сотрудник(Employee)***: слабая сущность, которая связана с сильной сущностью  ***Магазин(Shop)*** и не может существовать без неё, так же от этой сущности зависит сущность ***Заказ(Order)***. Содержит в себе информацию о сотруднике. Имеет следующие атрибуты:
- id_employee(integer) – простой, однозначный атрибут, в котором хранится номер сотрудника, является составляющим первичного ключа;
- id_shop (integer) - простой, однозначный атрибут, который ссылается на атрибут id_shop сущности  Магазин(Shop), в каком магазине работает сотрудник. Является внешним ключом и составляющей первичного ключа;
- fio(varchar(100)) - простой, многозначный атрибут, в котором хранятся ФИО сотрудника;
- phonenum(char(11)) - простой, однозначный атрибут, в котором хранится телефонный номер сотрудника;

***Покупатель(Buyer)***: сильная сущность, которая связана с слабой сущностью ***Заказ(Order)***. Хранит данные о покупателе. Содержит следующие атрибуты:
id_buyer(integer) - простой, однозначный атрибут, в котором содержится идентификатор покупателя. Является первичным ключом;
- phonenum(char(11)) - простой, однозначный атрибут, в котором хранится телефонный номер покупателя;
- bname(varchar(50)) - простой, многозначный атрибут, в котором хранится имя покупателя;

***Издатель(Publisher)***: сильная сущность, от которой зависят слабая сущность ***Игра(Game)***. Содержит в себе информацию о издателе настольных игр, имеет следующие атрибуты:
- id_publisher(integer) - простой, однозначный атрибут, в котором содержится идентификатор издателя. Является первичным ключом;
- name(varchar(100)) - простой, однозначный атрибут, в котором хранится название издателя; 

***Игра(Game)***: слабая сущность, которая зависит от сильной сущности ***Издатель(Publisher)*** и не может существовать без неё. Кроме того, сущность ***Заказ(Orders)*** зависит от данной сущности. Содержит в себе информацию о настольной игре, имеет следующие атрибуты:
- id_game(integer) - простой, однозначный атрибут, в котором содержится номер игры,  является составляющей первичного ключа;
- id_publisher(integer) - простой, однозначный атрибут, который ссылается на идентификатор сущности Издатель(Publisher), какое издательство издало это игру. Является внешним ключом и составляющей первичного ключа; 
- id_age_restriction(int) - простой, однозначный атрибут, который ссылается на идентификатор сущности Возрастное ограничение (Age_restriction), какой возрастной ценз у игры. Является внешним ключом и составляющей первичного ключа; 
- id_game_status(int) - простой, однозначный атрибут, который ссылается на идентификатор сущности Статус игры(Game_status). Является внешним ключом и составляющей первичного ключа; 
- name(varchar(60)) - простой, однозначный атрибут, в котором содержится название настольной игры
- playernum(integer) - простой, однозначный атрибут, в котором содержится требуемое кол-во игроков для игры
- price(integer) - простой, однозначный атрибут, в котором содержится цена настольной игры
- amount(int) - простой, однозначный атрибут, в котором содержится количество игр

***Заказ(Orders)***: слабая сущность, которая зависит от сущностей: ***Игра(Game), Покупатель(Buyer), Сотрудник(Employee)*** и не может существовать без них.Содержит в себе информацию о настольной игре, имеет следующие атрибуты:
- id_orders(integer) - простой, однозначный атрибут, в котором содержится номер заказа,  является составляющей первичного ключа;
- id_buyer(integer) - простой, однозначный атрибут, который ссылается на идентификатор сущности Покупатель(Buyer), какой покупатель купил сделал этот заказ. Является внешним ключом и составляющей первичного ключа; 
- id_game(varchar(60)) - простой, однозначный атрибут, который ссылается на идентификатор сущности Игра(Game), какая игра была куплена. Является внешним ключом и составляющей первичного ключа; 
- id_employee(integer) - простой, однозначный атрибут, который ссылается на идентификатор сущности Сотрудник(Employee), какой сотрудник оформил данный заказ. Является внешним ключом и составляющей первичного ключа; 
- id_order_status(int) - простой, однозначный атрибут, который ссылается на идентификатор сущности Статус заказа(Order_status). Является внешним ключом и составляющей первичного ключа;
- order_date(integer) - простой, однозначный атрибут, в котором содержится дата покупки

***Статус заказа(Order_status)***: сильная сущность, от которой зависят слабая сущность ***Заказ(Orders)***. Содержит в себе информацию о издателе настольных игр, имеет следующие атрибуты:
- id_order_status(int) - простой, однозначный атрибут, в котором содержится номер статуса заказа. Является первичным ключом;
- status(varchar(50)) - простой, однозначный атрибут, в котором содержится статус заказа;

***Статус игры(Game_status)***: сильная сущность, от которой зависят слабая сущность ***Игра(Game)***. Содержит в себе информацию о издателе настольных игр, имеет следующие атрибуты:
- id_game_status(int) - простой, однозначный атрибут, в котором содержится идентификатор статуса игры. Является первичным ключом;
- gamestatus(varchar(40)) - простой, однозначный атрибут, в котором содержится статус игры;

***Жанр игры(Game_genre)***:сильная сущность, от которой зависят слабая сущность ***Игра(Game)***. Содержит в себе информацию о издателе настольных игр, имеет следующие атрибуты:
- id_game_genre(int) - простой, однозначный атрибут, в котором содержится идентификатор жанра игры. Является первичным ключом;
- genre(varchar(30)) - простой, однозначный атрибут, в котором содержится жанр игры;

***Возрастное ограничение (Age_restriction)***: сильная сущность, от которой зависят слабая сущность ***Игра(Game)***. Содержит в себе информацию о издателе настольных игр, имеет следующие атрибуты:
- id_age_restriction(int) - простой, однозначный атрибут, в котором содержится идентификатор возрастного ценза. Является первичным ключом;
- age(int) - простой, однозначный атрибут, в котором содержится информация о возрастном ограничении игры.

Запросы
---

1. Игры дороже 2000 рублей, отсортированные по цене по убыванию
```sql
SELECT name, price
FROM game
WHERE price > 2000
ORDER BY price DESC
```
<details>
  <summary>
    Результат
  </summary>
  ![1](https://user-images.githubusercontent.com/120600282/208690066-c79bf906-0299-46a4-9eee-649cc16c81e1.jpg)
</details>

2. Какие магазины находятся в Москве?
```sql
SELECT city, address
FROM shop
WHERE city = 'Москва'
```
<details>
  <summary>
    Результат
  </summary>
  ![2](https://user-images.githubusercontent.com/120600282/208690096-a71b97a9-8382-4e36-8d55-ff943df8a395.jpg)
</details>

3. Кто работает на Кантемировской 3а?
```sql
SELECT employee.fio 
FROM employee, shop 
WHERE (employee.id_shop = shop.id_shop and shop.address='ул. Кантемировская, д.3а')
```
<details>
  <summary>
    Результат
  </summary>
  ![3](https://user-images.githubusercontent.com/120600282/208690129-15f85687-665d-4b9f-8cfc-dc94fd499380.jpg)
</details>

4. Какие игры принадлежат издательству “Звезда”?
```sql
SELECT game.name
FROM publisher LEFT JOIN game ON publisher.name='Звезда' AND publisher.id_publisher = game.id_publisher
```
<details>
  <summary>
    Результат
  </summary>
  ![4](https://user-images.githubusercontent.com/120600282/208690162-2bf3284d-dbfd-43b1-997a-7fb945b9acbc.jpg)
</details>

5. Сколько стоят игры издателя “Смарт”?
```sql
SELECT game."name", price, amount, price*amount as sum
FROM game JOIN publisher ON publisher.id_publisher = game.id_publisher
WHERE publisher."name" = 'Смарт'
```
<details>
  <summary>
    Результат
  </summary>
  ![5](https://user-images.githubusercontent.com/120600282/208690254-a3a794ba-e84e-4e22-8c4c-6e7855afae03.jpg)
</details>

6. Список покупателей, зарегистрировавшихся после 01.01.2014

```sql
SELECT *
FROM buyer
WHERE registration > '2014-01-01'
```
<details>
  <summary>
    Результат
  </summary>
  ![6](https://user-images.githubusercontent.com/120600282/208690275-9e9def81-1987-4848-9f3c-4e227eb5843a.jpg)
</details>

7. Статус заказов от 15.10.2013
```sql
SELECT id_orders, orders_date, status
FROM order_status JOIN orders ON orders.id_order_status = order_status.id_order_status
WHERE orders_date = '2013-10-15'
```
<details>
  <summary>
    Результат
  </summary>
  ![7](https://user-images.githubusercontent.com/120600282/208690293-3ecd0067-b3ce-466a-8f9e-336dfea65fc3.jpg)
</details>

8. Какие игры издателя “Смарт” сейчас есть в наличии?
```sql
SELECT game.name, publisher.name, amount, price
FROM publisher INNER JOIN game ON publisher.id_publisher = game.id_publisher
WHERE publisher.name = 'Смарт' AND game.amount > 0
ORDER BY amount DESC
```
<details>
  <summary>
    Результат
  </summary>
  ![8](https://user-images.githubusercontent.com/120600282/208690320-32b278cf-b68e-4293-b8e0-ff8bf0b368c1.jpg)
</details>

9. Топ-3 самых популярных жанра недели
```sql
SELECT genre, amount, orders_date
FROM game_genre, game, orders
WHERE orders_date < '2014-12-08'
ORDER BY amount DESC
LIMIT 3
```
<details>
  <summary>
    Результат
  </summary>
  ![9](https://user-images.githubusercontent.com/120600282/208690346-820231b1-1974-4aab-b1e1-98f443b6b15e.jpg)
</details>

10. В какой день недели какой жанр продавался?
```sql
SELECT publisher.name, genre, amount, EXTRACT(isodow FROM orders_date) as day_of_week
FROM publisher 
INNER JOIN game ON publisher.id_publisher = game.id_publisher 
INNER JOIN game_genre ON game.id_game_genre = game_genre.id_game_genre 
INNER JOIN orders ON game.id_game = orders.id_game 
ORDER BY amount DESC  
```
<details>
  <summary>
    Результат
  </summary>
  ![10](https://user-images.githubusercontent.com/120600282/208690385-b5899dad-8d28-4993-b127-51fb1bf68965.jpg)
</details>

11. Каких игр нет в наличии?
```sql
SELECT game.name, amount
FROM game
WHERE amount = 0
```
<details>
  <summary>
    Результат
  </summary>
  ![11](https://user-images.githubusercontent.com/120600282/208690412-a09a1323-d1be-49e9-9d2c-d5edbfc34de8.jpg)
</details>

12. Игры для детей младше 6 лет
```sql
SELECT game.name, age
FROM game JOIN age_restriction ON age_restriction.id_age_restriction = game.id_age_restriction
WHERE age < 6
```
<details>
  <summary>
    Результат
  </summary>
  ![12](https://user-images.githubusercontent.com/120600282/208690432-d417439f-7e89-45db-86fd-655209ad69c0.jpg)
</details>
