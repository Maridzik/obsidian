![[films.db]]

файл с таблицей

```python
python

import sqlite3

  

con = sqlite3.connect("films_db.sqlite")

cursor = con.cursor()

genres = cursor.execute('''SELECT id from genres WHERE title in("музыка", "анимация")''').fetchall()

genres = tuple([g[0] for g in genres])
 

films = cursor.execute(f'''SELECT title from films WHERE genre in {genres} AND year >= 1997''').fetchall()

for f in films:

print(f[0])

  

con.close()
```

sqlite3.connect("Название файла") - подключаем файл

cursor = con.cursor() - создаем курсор

con.close() - отключение файла
  

genres = cursor.execute('''SELECT id from genres WHERE title in("музыка",  "анимация")''').fetchall() - мы SELECT - ВЫБИРАЕМ столбец id из таблицы жанров ГДЕ столбец названия в ("музыка",  "анимация")


возвращается список с кортежами значений даже если оно одно.

```python

import sqlite3

  

  

def get_result(name):

con = sqlite3.connect(name)

cursor = con.cursor()

  

cursor.execute('''DELETE from films WHERE title LIKE "Я%а" ''')

con.commit()

con.close()


get_result("films_db.sqlite")
```

появляется новые DELETE - удаление

cursor.execute('''DELETE from films WHERE title LIKE "Я%а" ''') удаляем все строки где название КАК "Я%а" - начинается с Я и заканчивается а

con.commit() - сохраняем изменения в таблице