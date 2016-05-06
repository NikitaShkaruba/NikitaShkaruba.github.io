---
title: "M - Model in Rails"
ref: m-model-in-rails
layout: post
lang: en
---

#### СТАТЬЯ НЕДОПИСАНА!

### Реализация в Ruby on Rails
Object-Relational Mapping, commonly referred to as its abbreviation ORM, is a technique that connects the rich objects of an application to tables in a relational database management system. Using ORM, the properties and relationships of the objects in an application can be easily stored and retrieved from a database without writing SQL statements directly and with less overall database access code.

### Naming conventions
Convention over configuration - очень круто.

By default, Active Record uses some naming conventions to find out how the mapping between models and database tables should be created. Rails will pluralize your class names to find the respective database table. So, for a class Book, you should have a database table called books

Где как?
Database Table - Plural with underscores separating words (e.g., book_clubs).
Model Class - Singular with the first letter of each word capitalized (e.g., BookClub).

Короче, рельсы знает норм англ :D
|Class|Table|
|Article|articles|
|LineItem|line_items|
|Deer|deers|
|Mouse|mice|
|Person|people|

Foreign keys - These fields should be named following the pattern singularized_table_name_id (e.g., item_id, order_id). These are the fields that Active Record will look for when you create associations between your models.
Primary keys - By default, Active Record will use an integer column named id as the table's primary key. When using Active Record Migrations to create your tables, this column will be automatically created.

### Как же создать ActiveRecord класс?Что же такое
Короче, просто наследуемся от ActiveRecord::Base.
Даже не нужно никаких полей создавать, ActiveRecord возьмёт bз сущности всё сама.

```ruby
class MyHoe < ActiveRecord::Base
end
```

### Миграции
миграции - изменения базы данных.
Можно писать миграции не на языке SQL, а на обёртке над ним - Ruby DSL(domain specific language).

Пример миграции:

Можно очень удобно добавлять новые модели при помощи генерторов. Rails сделает всё сам.

```bash
 $ bin/rails generate model Product name:string description:text

# result
 class CreateProducts < ActiveRecord::Migration
  def change
    create_table :products do |t|
      t.string :name
      t.text :description

      t.timestamps null: false
    end
  end
end
```

К генераторам можно целять модификаторы колонок. Чтобы, к примеру, разрешать null в ней, задавать
точно десятичных чисел, ограничивать количество символов или цифр, добавлять дефолтные значения.

```ruby
$ rails generate migration AddDetailsToProducts 'price:decimal{5,2}'
```

### Почему именно Postgresql?
Ну блин, мне сказали, мол, в проекте используем PostgreSQL, я и начал её смотреть :smile:
Вообще, PostgreSQL - объектно-реляционная и бесплатная. В отличие от той-же mySQL.

### Простой проект
Итак, для начала, необходимо удостовериться, что все надлежащие пакеты установлены.

Настраиваем PostgreSQL.

```bash
# Обновляем доступные пакеты нашего пакетного менедера
$ sudo apt-get update
# Ставим PostgreSQL и его разрабатываемые библиотеки
$ sudo apt-get install postgresql postgresql-contrib libpq-dev
# Создаём пользователя нашей субд
$ sudo -u postgres createuser -s pguser --password
```

Если у вас не стоит Ruby, то ставим его, вот [статья](/youGotFooled) от меня, разбирающая Ruby Development Kit, т.е. те утилиты, которыми
ты будешь пользоваться, используя Руби

Создаём простое rails-приложение

```bash
$ cd ~/Code/RailsSamples/
$ rails new postgresql_sample_app -d postgresql
$ cd postgresql_sample_app

# Ставим нашего созданного пользователя оператором СУБД
$ vim config/database.yml
# Ищем там строку pool: 5 и добавляем следующее, заменяя pguser и pguser_password на свои.
  host: localhost
  username: pguser
  password: pguser_password
# Сохрняем и выходим.

# Создаём базы данных development и test
$ rake db:create

# Тестируем. После исполнения следующего идём браузером по localhos:3000
$ rails server
```

Если всё взлетело, то бд успешно установлена, и теперь её можо использовать,
как и любую другую.

#### Ну всё, ты успешен!
Теперь можно делать что захочешь. Допишу в течении недели.
