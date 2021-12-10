---
theme: default
highlighter: shiki
lineNumbers: false
title: 'Индексируем базу: как делать хорошо и не делать плохо'
info: |
  Индексируем базу: как делать хорошо и не делать плохо
fonts:
  provider: 'none'
  fallback: false
  local: 'Martian Grotesk,Martian Mono'
  sans: 'Martian Grotesk'
  serif: 'Martian Grotesk'
  mono: 'Martian Mono'
drawings:
  persist: false

layout: cover
---

# Индексируем базу<br /><small>как делать <span class="wobbling wobbling-a">хорошо</span><br />и не делать <span class="wobbling wobbling-b">плохо</span></small>

<div class="absolute bottom-0 my-2">
Новиков Андрей<br />
<small><a href="https://kommunity.com/saintpruby/events/fall-2021-meetup-26df1ea3">Winter Saint P 2021 meetup</a></small>
</div>

<div class="absolute bottom-0 right-0 h-40 scaled-image flex">
  <a href="https://evilmartians.com/" class="w-40 h-40 p-3"><img alt="Evil Martians" src="/images/01_Evil-Martians_Logo_v2.1_RGB.svg" /></a>
  <a href="https://kommunity.com/saintpruby" class="w-40 h-40"><img alt="Saint P Ruby Community" src="/images/saintpruby-logo.png" /></a>
</div>

<style>
  a { border-bottom: none !important; }

  .wobbling {
    animation-duration: 1s;
    animation-name: wobbling;
    animation-iteration-count: infinite;
    animation-direction: alternate;
  }

  .wobbling-a {
    animation-direction: alternate;
  }

  .wobbling-b {
    animation-direction: alternate-reverse;
  }

  @keyframes wobbling {
    from {
      font-stretch: 3%;
    }

    to {
      font-stretch: 9%;
    }
  }
</style>

<!--
Ну что, поговорим ещё немного про базы данных? Не отнекивайтесь, я же вижу — вы хотите этого.
-->

---
layout: full
---

<a href="https://github.com/Envek/"><img src="/images/github-envek.png" class="object-contain text-center m-auto h-full w-full max-h-full max-w-full" /></a>

<!--
Всем привет! Меня зовут Андрей…
-->

---

<a href="https://evilmartians.com/"><img alt="Evil Martians" src="/images/evil-martians-px.svg" class="object-contain text-center m-auto max-h-112"/></a>

<!--
…и я тоже Марсианин.
-->

---

<a href="https://evilmartians.com/"><img alt="Piter Martians" src="/images/Evil-Martians_Logo_Piter.png" class="object-contain text-center m-auto max-h-112"/></a>

<!--
Марсиане любят Питер. У нас даже офис был в Питере, только мы его закрыли, так как никто в него не хоодил. Удалёнщики мы до мозга костей, что поделать.
-->

---

# Марсианский Open Source

<div class="grid grid-cols-4 grid-rows-2 gap-4">
  <a href="https://github.com/yabeda-rb/yabeda">
    <figure>
      <img alt="Yabeda" src="/images/martian-oss/yabeda.svg" class="scaled-image h-40 mx-auto" />
      <figcaption>Yabeda: Ruby application instrumentation framework</figcaption>
    </figure>
  </a>
  <a href="https://github.com/evilmartians/lefthook">
    <figure>
      <img alt="LeftHook" src="/images/martian-oss/lefthook.svg" class="scaled-image h-40 mx-auto" />
      <figcaption>Lefthook: git hooks manager</figcaption>
    </figure>
  </a>
  <a href="https://anycable.io/">
    <figure>
      <img alt="AnyCable" src="/images/martian-oss/anycable.svg" class="scaled-image h-40 mx-auto" />
      <figcaption>AnyCable: Polyglot replacement for ActionCable server</figcaption>
    </figure>
  </a>
  <a href="https://postcss.org/">
    <figure>
      <img alt="PostCSS" src="/images/martian-oss/postcss.svg" class="scaled-image h-40 mx-auto" />
      <figcaption>PostCSS: A tool for transforming CSS with JavaScript</figcaption>
    </figure>
  </a>
  <a href="https://imgproxy.net/">
    <figure>
      <img alt="Imgproxy" src="/images/martian-oss/imgproxy.svg" class="scaled-image h-40 mx-auto" />
      <figcaption>Imgproxy: Fast and secure standalone server for resizing and converting remote images</figcaption>
    </figure>
  </a>
  <a href="https://logux.io/">
    <figure>
      <img alt="Logux" src="/images/martian-oss/logux.svg" class="scaled-image h-40 mx-auto" />
      <figcaption>Logux: Client-server communication framework based on Optimistic UI, CRDT, and log</figcaption>
    </figure>
  </a>
  <a href="https://github.com/DarthSim/overmind">
    <figure>
      <img alt="Overmind" src="/images/martian-oss/overmind.svg" class="scaled-image h-40 mx-auto" />
      <figcaption>Overmind: Process manager for Procfile-based applications and tmux </figcaption>
    </figure>
  </a>
  <a href="https://evilmartians.com/oss">
    <figure>
      <div class="h-40 text-2xl flex items-center justify-center">
        <qr-code-vue value="https://evilmartians.com/oss" class="scaled-image w-full h-full mx-auto p-4" render-as="svg" />
      </div>
      <figcaption style="font-size: 0.5rem;">И многие другие на evilmartians.com/oss</figcaption>
    </figure>
  </a>
</div>

<style>
  a { border-bottom: none !important; }
  figcaption {
    font-size: 0.4rem;
    line-height: 1rem;
  }
</style>

<!--
Марсиане зарабатывают себе на хлеб в первую очередь заказной разработкой и консалтингом для разных клиентов, в основном штатовских стартапов, но нас вы скорее всего знаете по нашим опенсорс-проектам, которыми мы бесконечно гордимся и которые были извлечены из недр коммерческой разработки и мы усиленно используем их везде, где только можно. Используйте и вы.

Кстати, вот этот проект, Ябеда — моё детище.
-->

---

# Зачем мне знать про индексы?

А главное — нафига оно всё Ruby-разработчику?

 - Данные — главная ценность большинства приложений
 - Традиционные СУБД плохо масштабируются горизонтально.
 - Так сложилось, что разработчики на Ruby on Rails разрабатывают фичи целиком (включая модель данных)
 - И не всегда есть DBA под рукой

<br />

**Полезно понимать, как оно работает и что может, чтобы не положить продакшен раньше времени.**

<!--
Давайте же переходить к сути!

Типичное веб-приложение — это в целом этакая надстройка над базой данных. Потому что данные — это основная ценность приложения (если протеряете боевую базу, то можно тушить свет, закрывать стартап, брать портвейн и идти домой).

При этом традиционная база, как правило, является бутылочным горлышком в плане производительности и тяжело поддаётся горизонтальному масштабированию.

И, поскольку мы воспитаны рельсой, в которой есть генераторы моделек, миграции базы данных и вот эта вся прекрасная машинерия, до которой ещё не везде в джаве доросли, да и вообще подход к разработке такой фуллстековый, то мы привыкли сами разрабатывать себе модель данных (да и многие ли стартапы могут себе позволить полноценного DBA или архитектора?)

В общем, базы требуют повышенного к себе внимания. И хорошо бы не лажать с базой данных, чтобы была возможность дорасти до такой стадии, когда компания может себе позволить выделенного DBA.

Спойлер: да и порой проще заботать самим и стать самим себе DBA, чем дождаться этого момента.
-->

---

## Disclaimer

Доклад будет про PostgreSQL, но многие вещи справедливы и для других SQL (и даже порой NoSQL) систем управления базами данных.

<div class="text-9xl flex items-center justify-center my-28">
  <img alt="Evil Martians" src="/images/01_Evil-Martians_Logo_v2.1_RGB.svg" class="slidev-icon m-8" style="height: 1.2em; width: 1.2em;" />
  <twemoji-red-heart class="m-8" />
  <logos-postgresql class="m-8" />
</div>

<!--
Говорить об индексах мы будем на примере PostgreSQL, просто потому что Марсиане любят Постгрес! Впрочем, многое, очень многое справедливо и для других баз данных.
-->

---
layout: intro
---

# Что ещё за индексы?

Может, не надо, а?

---

## Зачем нужны индексы?

SQL — декларативный язык.

Пользователь говорит, _что_ хочет получить, СУБД определяет, _как_ выполнять запрос.

И мы можем ей помочь, дав вспомогательные «словари»!

<!-- Как именно хранить данные и обеспечивать к ним доступ СУБД решает сама, у разработчика доступа к этому может и не быть -->

---
layout: footnote
---

## И что же такое индекс?

Вторичная структура данных, которая не влияет на результат выполнения запросов\*, но может ускорить его выполнение.

Ещё индексы поддерживают ограничения целостности (первичные и уникальные ключи).

::footnote::

\* Наличие индекса может поменять порядок возвращаемых данных, если в запросе не указан ORDER BY, а планировщик решил использовать индекс.

<!--
Что значит вторичная — индекс не содержит в себе никакой информации, которую нельзя было бы получить из самой таблицы. Индекс можно удалить и пересоздать.

Порядок строк без указания ORDER BY не определён в стандарте SQL, поэтому это не баг, а деталь реализации.
-->

---

## Почему не заиндексировать всё?

 - Индексы занимают место
 - Индексы нужно обновлять
   - замедление вставок и обновлений
   - write amplification
 - полезны не всегда
   - планировщик может не захотеть их использовать
   - новый индекс может оказаться медленнее старого


<!--
Может появиться соблазн заиндексировать всё к чёртовой бабушке, но надо гнать от себя нэто наваждение.

И хоть то, что индексы занимают место и кажется и является на самом деле минорной штукой — диски сейчас дешёвые, но вот необходимость при каждом изменении индексируемых полей обновлять все причастные к нему индексы вполне может поставить на колени даже самый мощный сервер с дорогой СХД — пропускная способность ввода-вывода весьма ограничена и масштабируется ох как плохо (и дорого).
-->

---

## Всегда ли стоит использовать индекс?

<div class="absolute inset-0 text-2xl flex items-center justify-center nb">
  Ну, нет
</div>


<!-- Наверное, всё же не стоит использовать индексы бездумно -->

---
layout: footnote
footnoteClass: text-xs
---
## А когда не стоит?

 - Если размер таблицы мал\* (сотни/тысячи записей) и она не будет расти
 - Или если запрос выполняется редко и скорость его выполнения не критична
 - Если большинство строк отбрасываются другими условиями (мультитенантные таблицы)

::footnote::

\* Локально приходится использовать `SET enable_seqscan = off;`, чтобы заставить СУБД использовать индекс.

<!--
Не стоит навешивать индексы на крошечные таблицы — всякие там справочники в жалкую сотню записей.

СУБД даже не будет пытаться его использовать, потому что это лишние телодвижения (мы об этом поговорим буквально через минуту).

Не всегда стоит оптимизировать и работу редких индексов, которые раз в день или неделю собирают статистику, строят отчёты и тому подобная OLAP-нагрузка. Если же эти запросы настолько тяжёлые, что ложат вам сервер с базой каждую ночь, то лучше поднять реплику и гонять эти запросы на ней, чем навешивать индекс и портить производительность вставок в рабочее время.

Ну и отдельный кейс: если у вас мультитенантное приложение и, например, у вас все запросы работают всегда в скоупе одного пользователя (и у вас нет каких-то исключительно больших пользователей с полбазы размером), то вам нужен только индекс по условному `user_id` но про селективность мы тоже ещё поговорим.
-->

---

## А когда стоит?

 - Когда ускорение от индекса перевешивает накладные расходы от похода в индекс
   1. Когда надо выбрать небольшое количество данных от размера таблицы
   2. Результат нужно отсортировать
 - Когда индекс ещё помещается в оперативную память, а таблица — уже нет
 - Когда ожидается, что количество данных в таблице будет расти
 - Или это внешний ключ, по которому будут выполняться JOINы

<!--

Ну и отдельно давайте проговорим, когда индексы на самом деле нужны.

Главное, для чего эффективен индекс — это ситуация вида «нужно найти иголку в стоге сена». Когда из огромной таблицы вам нужно вытащить буквально одну, десять или сто записей. Ну, в общем, мало, по сравнению с размером самой таблицы. Вот это тот юзкейс, который действительно ускоряется очень значимо.

Второй важный случай — сортировка. Поскольку индекс по умолчанию, BTree, хранит в себе данные уже отсортированными, то достать их в порядке индекса — плёвое дело.

Не стоит забывать, что оперативная память всё ещё ощутимо быстрее дисков, даже SSD, поэтому обойти маленький индекс в памяти будет на порядки быстрее, чем сходить на диск за табличкой, которая уже может в память не помещаться.

Ну и JOIN'ы. Когда мы начинаем соединять таблицы без индекса, можно очень так квадратичненько попасть по сложности и поседеть раньше, чем запрос выполниться.

-->

---

## Падажжи

> когда надо выбрать небольшое количество данных относительно размера таблицы

А как СУБД это понимает?

**Статистика!**

СУБД знает о каждой колонке:
 - количество данных
 - их упорядоченность (корреляция)
 - количество разных значений
 - их количественное распределение (гистограмма)

И использует это при планировании запросов.

**Статистика безумно важна!**

<!-- Погодите-ка, что ещё знает обо мне СУБД, чего не знаю я? -->

---

## Как может выполнять запрос PostgreSQL

 - seq scan - обойти всю табличку на диске, страница за страницей
 - index only scan - достать все данные только из индекса
 - index scan - сходить в индекс, сходить в страницы на диске
 - bitmap index scan + heap scan — сходить в индекс, построить битовую карту интересных страниц, загрузить их все, отфильтровать…

## Как выбирает?

 - Планировщик перебирает варианты выполнения
 - считает примерную стоимость каждого (с учётом статистики)
 - выбирает самый дешёвый _(как ему кажется)_

<!-- Стоимость запроса считается в условных попугаях и складывается из ориентировочной времени, нужного на загрузку данных с диска и обработки данных в памяти. Если Акелла промахнётся с оценкой стоимости… -->

---

## Seq scan

Последовательно читаем всю таблицу, сразу отдаём данные клиенту пачками (используйте курсоры).

Просто, хорошо работает на HDD, линейное время.

Если данные нужно отсортировать — становится хуже.

---

## Index scan

Ищем требуемые данные в индексе, смотрим, где они лежат на диске, идём на диск, повторяем.

Логарифмическое время, чтобы найти данные в индексе, линейное — чтобы считать.

В случае стандартного BTree-индекса результат будет уже отсортирован.

---
layout: footnote
footnoteClass: text-xs
---

## Заглянем в индекс (BTree)

<img src="/images/btree-range-search.png" class="text-center m-auto object-scale-down max-h-84">

::footnote::

Источник: [Postgres Professional: курс «Оптимизация запросов»](https://postgrespro.ru/education/courses/QPT), тема №4 «Индексный доступ».

Подробнее: [Индексы в PostgreSQL — 4](https://habr.com/en/company/postgrespro/blog/330544/)

---

## Подстава!

В PostgreSQL даже в самой последней 14-й версии настройки планировщика по умолчанию заточены под работу на HDD:

> - `seq_page_cost (floating point) `
>
>    Sets the planner's estimate of the cost of a disk page fetch that is part of a series of sequential fetches. **The default is 1.0**.
>
> - `random_page_cost (floating point)`
>
>    Sets the planner's estimate of the cost of a non-sequentially-fetched disk page. **The default is 4.0**.

Это значит, что планировщик будет чаще выбирать seq scan при живом-то индексе!

Используйте [PgTune](https://pgtune.leopard.in.ua/)!

<qr-code url="https://pgtune.leopard.in.ua/" caption="pgtune.leopard.in.ua" class="absolute bottom-0 right-0 w-32" />

---
layout: footnote
footnoteClass: text-xs
---

## Bitmap index scan

Строится промежуточная битовая карта, чтобы читать страницы по одному разу.

<img src="/images/btree-bitmap-scan.png" class="text-center m-auto object-scale-down max-h-80">

::footnote::

Источник: [Postgres Professional: курс «Оптимизация запросов»](https://postgrespro.ru/education/courses/QPT), тема №5 «Сканирование по битовой карте».

Подробнее: [Индексы в PostgreSQL — 4](https://habr.com/en/company/postgrespro/blog/330544/)

<!-- Основная стоимость возникает при чтении страниц с диска (чтение, вытесненение, вот это всё) -->

---
layout: footnote
footnoteClass: text-xs
---

## Когда что используется?

<img class="text-center m-auto object-scale-down max-h-96" alt="Эффективность различных методов доступа в зависимости от селективности" src="/images/index-access-methods-efficiency.png" />

::footnote::

Источник: [Postgres Pro: курс «Оптимизация запросов»](https://postgrespro.ru/education/courses/QPT), тема №5 «Сканирование по битовой карте».

---

## Index only scan

Если все данные, нужные для запроса, лежат в индексе (и MVCC-звёзды сходятся), то можно даже не ходить на диск!

Но как этого достичь?

Спойлер: избегайте `SELECT *`

---

## Многоколоночные индексы

- число столбцов ограничено. 32

- BTree, GIN, GiST, SP-GiST

- Порядок столбцов важен!

```sql
CREATE INDEX ON users(account_id, age)

SELECT * FROM users WHERE account_id = 1 AND age < 30
SELECT * FROM users WHERE account_id = 1

CREATE INDEX ON users(account_id) -- не нужен!
CREATE INDEX ON users(age)        -- нужен!
```

---
layout: footnote
footnoteClass: text-xs
---

## Покрывающие индексы

Можно добавить лишних колонок в индекс, чтобы не пришлось ходить в таблицу, а всё сразу достать из индекса\*

PostgreSQL 11+ добавил поддержку `INCLUDE`, которая позволяет добавлять доп. данные в уникальные индексы:

```sql
CREATE UNIQUE INDEX index_fk_on_listings
  ON listings (`product_id`, site_id)
  INCLUDE (`id`);
```

Особенно полезно включать первичный ключ, что позволяет ускорять множественные JOIN'ы.

```sql
SELECT *
FROM products
JOIN listings           ON products.id = `listings.product_id`
JOIN listing_variations ON `listings.id` = listing_variations.listing_id
```

::footnote::

В ActiveRecord [фичу не добавили](https://github.com/rails/rails/pull/37515), а вот отдельный гем уже есть: [`activerecord-covering-index`](https://gitlab.com/schlock/activerecord-covering-index).

---
layout: footnote
---

## Размер имеет значение

<img src="/images/if-you-know-what-i-mean-meme.png" class="text-center m-auto object-scale-down max-h-96">

::footnote::

Чем **меньше** индекс, тем более он «привлекателен» для планировщика.

---

## Частичные индексы

Дано:

```ruby
class Listing < ActiveRecord::Base
  scope :published, -> { where.not(item_id: nil) }
end
```

Создадим два индекса: простой и частичный — с условием `WHERE item_id IS NOT NULL` (в таблице заполнено примерно 10% строк):

```sql
CREATE INDEX index_listings_on_item_id ON listings (item_id);

CREATE INDEX index_listings_on_item_id_not_null ON listings (item_id)
  WHERE item_id IS NOT NULL;
```

И… 🥁

---

## Частичные индексы

```sql {6,12}
example_database=# \di+ index_listings_on_*
-[ RECORD 1 ]-+----------------------------------
Name          | index_listings_on_item_id
Table         | listings
Access method | btree
Size          | 290 MB

-[ RECORD 2 ]-+----------------------------------
Name          | index_listings_on_item_id_not_null
Table         | listings
Access method | btree
Size          | 38 MB
```

Помним, что `NULL != NULL`, да?

```
example_database=# EXPLAIN SELECT * FROM listings WHERE item_id = '100500';

 Index Scan using index_listings_on_item_id_not_null on listings  (cost=0.14..8.16 rows=1 width=373)
   Index Cond: ((item_id)::text = '100500'::text)
```

<!--
Обычно запросы должны иметь такой же `WHERE`, но обратите внимание, что в WHERE нет условия на NOT NULL.
-->

---

## Функциональные индексы

```sql
CREATE UNIQUE INDEX username_constraints
  ON users (`LOWER(username)`);
```

 - позволяют ускорять запросы с точно таким же выражением в SELECT, WHERE или ORDER BY
 - позволяют как бы «закэшировать» производное значение
 - есть своя отдельная статистика
 - «дорогое» обслуживание
 - можно использовать самописные функции (они должны быть `IMMUTABLE`)

---
layout: footnote
---

## Использование нескольких индексов

Если в запросе идёт отбор по нескольким проиндексированным колонкам, то планировщик может построить несколько битовых карт и логически их объединить.

```sql
CREATE INDEX on t(a);
CREATE INDEX on t(b);
ANALYZE t;
EXPLAIN SELECT * FROM t WHERE a <= 100 AND b = 'a';
```

```
   Recheck Cond: ((a <= 100) AND (b = 'a'::text))
   ->  BitmapAnd
         ->  Bitmap Index Scan on t_a_idx
               Index Cond: (a <= 100)
         ->  Bitmap Index Scan on t_b_idx
               Index Cond: (b = 'a'::text)
```

::footnote::

[habr.com/ru/company/postgrespro/blog/326096](https://habr.com/ru/company/postgrespro/blog/326096/)

<qr-code url="https://habr.com/ru/company/postgrespro/blog/326096/" caption="habr.com/ru/company/postgrespro/blog/326096" class="absolute bottom-0 right-0 w-36" />

---
layout: intro
---

# Я слышал, они разные бывают

BTree, Hash, GIN, GiST, SP-GiST, BRIN, Bloom, RUM, что, зачем, почему?

---
layout: footnote
---

## BTree

 - cбалансированное дерево
 - сильно ветвистое (много дочерних узлов)
 - двусвязный список из листьев одного уровня

<img class="m-auto text-center object-scale-down h-max-72" src="/images/b-tree.png" />

::footnote::
[habr.com/ru/company/postgrespro/blog/330544](https://habr.com/ru/company/postgrespro/blog/330544/)

<!--
минимизация дисковых операций на блочных устройствах

Лучше работает в случае последовательных id и хуже — в случае случайных UUID.
-->

---
layout: footnote
---

## BTree

Сложность поиска: O(log(n))

Операции: `<`, `<=`, `=`, `>=`, `>`, `IN`, `BETWEEN`, `IS NULL`, `IS NOT NULL`, `LIKE 'smth%'`, `~ '^smth'`

Бонус: ускоряет `ORDER BY`, поддерживает уникальность

Для первичных ключей лучше работает в случае последовательных id и хуже — в случае случайных UUID.

::footnote::
[habr.com/ru/company/postgrespro/blog/330544](https://habr.com/ru/company/postgrespro/blog/330544/)

<qr-code url="https://habr.com/ru/company/postgrespro/blog/330544/" caption="habr.com/ru/company/postgrespro/blog/330544" class="absolute bottom-0 right-0 w-48" />

---
layout: footnote
---

## Hash

Сложность поиска: O(1)

Операции: только `=`

Компактнее, чем B-Tree, но быстрее только на _очень_ больших таблицах и на выборках единичных значений.

Не поддерживает уникальность :-(

<img class="m-auto text-center" src="/images/hash-index.png" />

<div class="text-xs">

**Осторожно!** В бою можно использовать только начиная с PostgreSQL 10 (но это самая старая версия из поддерживаемых)
</div>

::footnote::
Подробнее: [habr.com/ru/company/postgrespro/blog/328280](https://habr.com/ru/company/postgrespro/blog/328280/)

<!--
Не поддерживает уникальность и все операции неравенства.

Его вообще реализовали «до кучи» — ну раз уж у нас хэш-функция, давайте сделаем и индекс на её основе. И долгое время не уделяли внимания и в итоге была непонятная и не очень юзабельная штука.

Планировщик и сейчас предпочитает выбирать B-Tree на не очень бальших таблицах.
-->

---
layout: footnote
---

## GIN

- Generalized Inverted Index

- Внутри BTree, содержащее составные значения (пример: лексемы слов) и список/дерево со ссылками на строки

- Подходит для составных объектов, которые бьются на простые составляющие

- Может расширяться под различные типы данных

<br/>

### Operations

hstore: `@>`, `?`, `?&`, `?|`

jsonb: `@>`, `?`, `?&`, `?|`

array: `<@`, `@>`, `=`, `&&`

::footnote::
[habr.com/ru/company/postgrespro/blog/340978](https://habrahabr.ru/company/postgrespro/blog/340978/)

<qr-code url="https://habrahabr.ru/company/postgrespro/blog/340978/" caption="habr.com/ru/company/postgrespro/blog/340978" class="absolute bottom-0 right-0 w-48" />

<!--
@> - contains
<@ - is contained

Не поддерживает сортировку и поиск по диапазонам

Оно бы хорошо подходило для внешних ключей, но пухнет ощутимо сильнее B-Tree и надо его иногда перестраивать.
-->

---
layout: footnote
---

## GIN

<img class="m-auto h-auto w-auto object-scale-down text-center max-h-96" src="/images/gin-tree.png" />

::footnote::
Источник: [habr.com/ru/company/postgrespro/blog/340978](https://habrahabr.ru/company/postgrespro/blog/340978/)


---
layout: footnote
---

## GiST

- Generalized Search Tree, настраиваемое

- Инфраструктура под разные типы данных и операторов (B-trees, R-trees)

- Геометрически данные (box, circle, point, polygon), полнотекстовый поиск (tsquery, tsvector)

- Не включает в себя данные, но включает в себя _предикат_, которому данные удовлетворяют

- Operations: `<<`, `>>`, `~=`, `<^`, `>^`, `<->`, `<@`, `@>`

- Для поддержки `=`, `<`, `>` нужно включать расширение `btree_gist`

- Поддерживает exclusion constraint (как unique, но на интервалах)

::footnote::
[habr.com/ru/company/postgrespro/blog/333878/](https://habrahabr.ru/company/postgrespro/blog/333878/)

<qr-code url="https://habrahabr.ru/company/postgrespro/blog/333878/" caption="habr.com/ru/company/postgrespro/blog/333878" class="absolute bottom-0 right-0 w-48" />


<!--

Generalized — в том смысле, что позволяет на основе себя строить и B-Tree и другие типы индексов.

B-Tree жёстко завязано на семантику операций «больше», «меньше», «равно», что хорошо работает для чисел и посимвольного сравнения строк, но когда нужно работать хотя бы с двухмерными данными, для которых смысл имеют совсем другие операции, становится нужен GiST.

Обратите внимание, что GiST из коробки не поддерживает операторы от B-Tree, их надо включать отдельно

Позволяет работать с геоданными

Exclusion constraints — классная возможность, которую как раз даёт GiST. Можно на уровне базы железобетонно обеспечить непересекаемость интервалов времени или областей на карте. Т.е. реализовать бронирование переговорок и база данных не даст вам забронировать одну и ту же переговорку на одно и то же время.

-->

---
layout: footnote
---

## GiST

<img class="m-auto h-auto w-auto object-scale-down text-center max-h-96" src="/images/gist-tree.png" />

::footnote::
Источник: [habr.com/ru/company/postgrespro/blog/333878/](https://habrahabr.ru/company/postgrespro/blog/333878/)

---
layout: footnote
---

## GiST

<img class="m-auto h-auto w-auto object-scale-down text-center max-h-96" src="/images/gist-for-map.png" />

::footnote::
Источник: [habr.com/ru/company/postgrespro/blog/333878/](https://habrahabr.ru/company/postgrespro/blog/333878/)

---
layout: footnote
---

## SP-GiST

- Space-Partitioned GiST

- Инфраструктура для несбалансированных многомерных непересекающихся структур

- Префиксные деревья и прочие естественно непересекающиеся штуки

- Может быть значительно компактнее BTree для префиксного поиска

- Внутри себя хранит _метки_ и _префиксы_, по которым идёт поиск

- PG 9.2+

::footnote::

Подробнее: [habr.com/ru/company/postgrespro/blog/337502](https://habrahabr.ru/company/postgrespro/blog/337502/)

<qr-code url="https://habrahabr.ru/company/postgrespro/blog/337502/" caption="habr.com/ru/company/postgrespro/blog/337502" class="absolute bottom-0 right-0 w-48" />

---
layout: footnote
---

## SP-GiST

<img class="m-auto h-auto w-auto object-scale-down text-center max-h-96" src="/images/sp-gist-for-map.png" />

::footnote::
Источник: [habr.com/ru/company/postgrespro/blog/337502](https://habrahabr.ru/company/postgrespro/blog/337502/)

---
layout: footnote
---

## SP-GiST

<img class="m-auto text-center max-h-96" src="/images/sp-gist-tree.png" />

::footnote::
Источник: [habr.com/ru/company/postgrespro/blog/337502](https://habrahabr.ru/company/postgrespro/blog/337502/)

---
layout: footnote
---

## BRIN

- Block Range Index

- Очень большие таблицы, естественно сортированные

- Хранит MIN и MAX значений колонки в каждой странице

  начиная с PG 14 хранит несколько интервалов

- Очень компактный и дешёвый в обслуживании

- PG 9.5+

::footnote::
Подробнее: [habr.com/ru/company/postgrespro/blog/346460](https://habrahabr.ru/company/postgrespro/blog/346460/)

<qr-code url="https://habrahabr.ru/company/postgrespro/blog/346460/" caption="habr.com/ru/company/postgrespro/blog/346460" class="absolute bottom-0 right-0 w-48" />

<!--
Суть индекса в компромиссе между скоростью работы и размером. Индекс позволяет отсеять бо́льшую часть таблицы.

минимальные и максимальные значения, встречающиеся в индексированном столбце в определённой зоне
-->

---
layout: footnote
---

## Bloom

 - Строятся битовые сигнатуры по хэш-функции от значений

 - Вероятностный индекс с нестабильной производительностью

   Индекс даёт false positives и лишние чтения с диска

 - Поддерживается только `=`, но можно искать по многим колонкам

 - Больше, чем BRIN, но компактнее чем Hash

 - Компромиссное решение для очень больших таблиц

 - Нужно подбирать параметры

 - PG 9.6+

::footnote::

Подробнее: [habr.com/ru/company/postgrespro/blog/349224](https://habr.com/ru/company/postgrespro/blog/349224/)

<qr-code url="https://habr.com/ru/company/postgrespro/blog/349224/" caption="habr.com/ru/company/postgrespro/blog/349224" class="absolute bottom-0 right-0 w-48" />

---
layout: footnote
---

## RUM

- GIN 2.0

- вместе с номерами строк хранится дополнительная информация, например, расстояние между словами

- Можно считать релевантность прямо в индексе и делать фразовый поиск (когда порядок слов важен)

- Нет в стандартной поставке — нужно ставить отдельно.

- PG 9.6+

::footnote::
Исходники: [github.com/postgrespro/rum](https://github.com/postgrespro/rum)

Подробнее: [https://habr.com/ru/company/postgrespro/blog/343488](https://habr.com/ru/company/postgrespro/blog/343488/)

<qr-code url="https://habr.com/ru/company/postgrespro/blog/343488/" caption="habr.com/ru/company/postgrespro/blog/343488" class="absolute bottom-0 right-0 w-48" />

---

## Экзотика

 - [ZomboDB](https://github.com/zombodb/zombodb) — ElasticSearch как индекс в БД

   ```sql
   CREATE EXTENSION zombodb;

   CREATE INDEX idxproducts
       ON products
    USING zombodb ((products.*))
     WITH (url='localhost:9200/');

   SELECT *
     FROM products
    WHERE products ==> '(keywords:(sports OR box) OR long_description:"wooden away"~5) AND price:[1000 TO 20000]';
   ```

<qr-code url="https://github.com/zombodb/zombodb" caption="github.com/zombodb/zombodb" class="absolute bottom-0 right-0 w-42" />

---

## Итого

BTree — Для большинства типов и запросов

GIN — Для JSONB/hstore/arrays/полнотекстового поиска

GiST — Для геометрии/географии/exclusion constraints/полнотекстового поиска

SP-GiST — Для геометрии/географии/exclusion constraints/префиксного поиска

Hash — Для `=`, но стоит ли?

BRIN — для больших естественно-отсортированных (write-only) таблиц

Bloom — для поиска по многим колонкам в огромных таблицах

RUM — для фразового полнотекстового поиска

---
layout: intro
---

# Индексы в миграциях

или ~~тысяча и~~ всего один способ положить продакшен (зато какой!)

---

## А в чём проблема в миграциях?

**Блокировки!** Создание индекса в PG блокирует таблицу на запись целиком.

Запросы, которые хотят записать в эту же таблицу встают в очередь за блокировкой…

Пока все пулы соединений не исчерпаются.

Вуаля! Мы лежим! 🤡

<hr />

Транзакционный DDL — благо, но блокировки отпускаются только в конце транзакции.

---

## А что делать?

Отказаться от транзакционного DDL и создавать индексы конкурентно.

```ruby {2,5}
class AddMissingIndexes < ActiveRecord::Migration[6.1]
  disable_ddl_transaction!

  def change
    add_index :big_table, %i[column], algorithm: :concurrently
  end
end
```

---
layout: footnote
---

## Всё равно всё встаёт «колом»?

`CREATE INDEX CONCURRENTLY` всё равно берёт блокировку всей таблицы, чтобы её тут же отпустить, но если в таблицу активно пишут другие долгие транзакции, то следом за ждущим блокировки `CREATE INDEX` скопятся очередь из других запросов и… 💥

### ~~Хак~~ решение

Снимайте нагрузку перед накаткой любых миграций на нагруженные таблицы — останавливайте Sidekiq, …

::footnote::

И избегайте долгих транзакций! Гем [isolator](https://github.com/palkan/isolator) вам в помощь!

<qr-code url="https://github.com/palkan/isolator" caption="gem isolator" class="absolute bottom-0 right-0" />

---
layout: footnote
---

## Как не пропустить плохую миграцию?

1. Используйте линтеры:

```ruby
gem "strong_migrations"
```

Анализирует ваши миграции и подскажет, когда они могут быть опасны на продакшене.

```
=== Dangerous operation detected #strong_migrations ===

Adding an index non-concurrently blocks writes. Instead, use:

class AddMissingIndexes < ActiveRecord::Migration[6.1]
  disable_ddl_transaction!

  def change
    add_index :table, :column, algorithm: :concurrently
  end
end
```

::footnote::

[github.com/ankane/strong_migrations](https://github.com/ankane/strong_migrations)

<qr-code url="https://github.com/ankane/strong_migrations" caption="gem strong_migrations" class="absolute bottom-0 right-0" />

<!-- Ну как, подскажет, просто выкинет эксепшен -->

---

## Как не пропустить плохую миграцию?

2. Гоняйте миграции на CI:

```yaml {10}
  db-linters:
    steps:
      - attach_workspace:
          at: .
      - run:
          name: Backup db/structure.sql to compare for changes later
          command: cp -f db/structure.sql{,.bak}
      - run:
          name: Check that migrations are not broken
          command: bundle exec rails db:create db:migrate
      - run:
          name: Check that db/structure.sql is up to date (there should be no changes)
          command: git diff --exit-code --no-index -- db/structure.sql{.bak,}
      - run:
          name: Ensure seeds are valid
          command: bundle exec rails db:seed
```

---
layout: footnote
---

## Итого: «правила буравчика» 👍

 1. Накладывайте индексы на внешние ключи

    Хорошая новость: `add_reference` в миграциях уже их добавляет

    Для таблиц, используемых в JOIN'ах «посередине», добавляйте первичный ключ в индекс для index only scan.

 2. Делайте частичные индексы, если большинство строк в таблице ожидаются пустыми.

 3. Не добавляйте индексы для OLAP-запросов (построение отчётов по всем данных и т.п.)

 4. Удаляйте дублирующие и неиспользуемые индексы \*

::footnote::

\* [wiki.postgresql.org/wiki/Index_Maintenance](https://wiki.postgresql.org/wiki/Index_Maintenance)

<qr-code url="https://wiki.postgresql.org/wiki/Index_Maintenance" caption="PG Index Maintenance" class="absolute bottom-0 right-0" />

---

## Что почитать?

 1. The Art of PostgreSQL: [theartofpostgresql.com](https://theartofpostgresql.com)

 2. Use the Index, Luke:   [use-the-index-luke.com](https://use-the-index-luke.com)

 3. Postgres Professional: курс «Оптимизация запросов»

    [postgrespro.ru/education/courses/QPT](https://postgrespro.ru/education/courses/QPT)

 4. Цикл статей «Индексы в PostgreSQL»

    [habr.com/ru/company/postgrespro/blog/326096](https://habr.com/ru/company/postgrespro/blog/326096/)

<div class="grid grid-cols-4 mt-4">
  <qr-code url="https://theartofpostgresql.com" caption="1. The Art of PostgreSQL" class="w-36" />
  <qr-code url="https://use-the-index-luke.com" caption="2. Use the Index, Luke" class="w-36" />
  <qr-code url="https://postgrespro.ru/education/courses/QPT" caption="3. Оптимизация запросов" class="w-36" />
  <qr-code url="https://habr.com/ru/company/postgrespro/blog/326096/" caption="4. Индексы в PostgreSQL" class="w-36" />
</div>

---

## P.S> Обновляйтесь!

 - PostgreSQL 14: уменьшение распухания BTree, улучшение BRIN
 - PostgreSQL 13: дедупликация значений в BTree (круто для foreign key)
 - PostgreSQL 12: покрывающие GiST-индексы, `REINDEX CONCURRENTLY`
 - PostgreSQL 11: покрывающие индексы (кроме GiST), партиционированные индексы
 - PostgreSQL 10: параллельное сканирование BTree, полноценные Hash-индексы
 - PostgreSQL 9.6: ☠️ (алло, вы уже должны были обновиться с неё!)

<style>
  ul li { margin-bottom: 0.5rem; }
</style>

---
layout: footnote
---

## Минутка нативной рекламы

Это (и многое-многое другое) мы можем в вас насильно впихнуть под давлением на наших фирменных курсах Brainwashing.

<img class="mx-auto my-12 text-center max-h-36" src="/images/brainwashing.png" />

В последний раз я рассказывал про базы данных 4 (четыре) часа подряд.

Проведём весной, если эпидемиологическая ситуация позволит 🤞

::footnote::

Записывайтесь в добровольцы на [brainwashing.pro/rails](https://brainwashing.pro/rails).

<qr-code url="https://brainwashing.pro/rails?utm_source=saintprug&utm_medium=slides&utm_campaign=indexes-2021" caption="brainwashing.pro/rails" class="absolute bottom-0 right-0 w-40" />

---
layout: footnote
---

## Нам нужны твои мозги!

<img class="mx-auto text-center max-h-96" src="/images/evl-ms-jobs-qrcode.png" />

::footnote::

Пункт призыва на галактическую службу по контракту: [evl.ms/jobs](https://evl.ms/jobs/)

<!-- но если не хочется ждать и платить деньги за курсы, есть отличная возможность получить эти же знания в бою, да ещё и с приличным жалованьем в придачу! Придётся присягнуть на верность Императору и отправиться покорять дальние миры в Галактике, но поверьте, оно того стоит! -->

---

# Внимание! Внимание!
## Спасибо за внимание!

<div class="grid grid-cols-4 grid-rows-3 mt-16 gap-4">

<div class="justify-self-end">
<img alt="Andrey Novikov" src="https://secure.gravatar.com/avatar/d0e95abdd0aed671ebd0920c16d393d4?s=512" class="w-32 h-32 scaled-image" />
</div>

<ul class="list-none col-span-2">
<li><a href="https://github.com/Envek"><logos-github-icon /> @Envek</a></li>
<li><a href="https://t.me/envek"><logos-telegram /> @Envek</a></li>
<li><a href="https://twitter.com/Envek"><logos-twitter /> @Envek</a></li>
<li><a href="https://www.instagram.com/Envek"><logos-instagram-icon /> @Envek</a></li>
</ul>

<div>
<qr-code url="https://github.com/Envek" caption="github.com/Envek" class="w-36" />
</div>

<div class="justify-self-end row-span-2">
<a href="https://evilmartians.com/"><img alt="Evil Martians" src="/images/01_Evil-Martians_Logo_v2.1_RGB.svg" class="w-32 h-32 scaled-image" /></a>
</div>

<div class="row-span-2 col-span-2">

- <logos-telegram />  [@evilmartians](https://t.me/evilmartians)
- <logos-twitter /> [@evilmartians_ru](https://twitter.com/evilmartians_ru/)
- <logos-instagram-icon /> [@evil.martians](https://www.instagram.com/evil.martians/)

Вакансии: [evilmartians.com/jobs](https://evilmartians.com/jobs/)

Блог: [evilmartians.com/chronicles](https://evilmartians.com/chronicles/)
</div>

<div>
<qr-code url="https://taplink.cc/evil.martians" caption="Evil Martians: links" class="w-36" />
</div>
</div>

<style>
  ul a { border-bottom: none !important; }
  ul { list-style-type: none !important; }
  ul li { margin-left: 0; padding-left: 0; }
</style>
