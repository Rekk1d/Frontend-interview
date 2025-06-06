# Структуры данных

Структуры нужны, чтобы упорядочивать, искать, анализировать и использовать данные с применением алгоритмов программирования.

## Массив (Array)

На массивах основаны многие другие структуры данных: списки, стеки, очереди.

Массивы бывают двух видов:

- Одномерные

У каждого элемента только один индекс. Можно представить это как строку с данными, где одного номера достаточно, чтобы чётко определить положение каждой переменной.

- Многомерные

У каждого элемента два или больше индексов. По сути, это комбинация из нескольких одномерных массивов, то есть вложенная структура.

Временная сложность

| Алгоритм | Среднее значение | Худший случай |
|----------|------------------|---------------|
| Space    | O(n)             | O(n)         |
| Search   | O(n) / O(log n)  | O(n)         |
| Insert   | O(n) / O(1)      | O(1)         |
| Delete   | O(1) / O(n)      | O(1)         |


## Динамический массив (Dynamic array)

Динамический массив — это тот, у которого размер может изменяться. При его создании задаётся максимальная величина и количество заполненных элементов. При добавлении новых элементов они сначала заполняются до максимальной величины, а при превышении сразу создаётся новый массив, с большей максимальной величиной.

Элементы в динамический массив можно добавлять без ограничений и куда угодно. Однако, если добавлять их в середину, остальные придётся сдвигать, что занимает много времени. Поэтому лучше всего динамический массив работает при добавлении элементов в конце.

## Связный список (Linked list)

Связный список — это группа из узлов. В каждом узле содержатся:
- Данные.
- Указатель или ссылка на следующий узел.
- В некоторых списках — ещё и ссылка на предыдущий узел.

Как применяют связные списки:
- Для построения более сложных структур данных.
- Для реализации файловых систем.
- Для формирования хэш-таблиц.
- Для выделения памяти в динамических структурах данных.

Временная сложность

| Алгоритм | Среднее значение | Худший случай |
|----------|------------------|---------------|
| Space    | O(n)             | O(n)         |
| Search   | O(n)             | O(n)         |
| Insert   | O(1)             | O(1)         |
| Delete   | O(1)             | O(1)         |

## Стек (Stack)

Эта структура данных позволяет добавлять и удалять элементы только из начала. Она работает по принципу LIFO — Last In, First Out (англ. «последним пришёл — первым ушёл»)

Как применяют стеки:
- Для реализации рекурсии.
- Для вычислений постфиксных значений.
- Для временного хранения данных, например истории запросов или изменений.

Временная сложность

| Алгоритм | Среднее значение | Худший случай |
|----------|------------------|---------------|
| Space    | O(n)             | O(n)         |
| Search   | O(n)             | O(n)         |
| Insert   | O(1)             | O(1)         |
| Delete   | O(1)             | O(1)         |


## Очередь (Queue)

Этот вид структуры представляет собой ряд данных, как и стек. Но в отличие от него она работает по принципу FIFO — First In, First Out (англ. «первым пришёл — первым ушёл»).

Бывают неклассические, двусторонние очереди. В них можно добавлять элементы и извлекать их из начала и конца структуры. Элементы посередине недоступны.

Как применяют очереди:

- Для реализации очередей, например на доступ к определённому ресурсу.

- Для управления потоками в многопоточных средах.

- Для генерации значений.

- Для создания буферов.


## Множество (Set)

Во множестве данные не упорядочены. Они хранятся группой, их нельзя структурировать и в некоторых случаях нельзя сортировать. Зато с ними можно работать как с классическими математическими множествами: объединять, искать пересечения, вычислять разность и смотреть, является ли одно множество подмножеством другого.

Как применяют множества:
- Для поддержания множества уникальных элементов.
- Для хранения данных, которые не нужно сортировать.
- Для сравнения, объединения наборов данных и других операций с ними.

## Карта (Map)

Её ещё называют ассоциативным массивом или словарём. Данные здесь хранятся в паре «ключ/значение», причем каждый ключ уникален, а вот значения могут повторяться. То есть определённому уникальному ключу всегда соответствует конкретное значение.

Как применяют Карту:
- Для быстрого поиска данных.
- Для создания баз, в которых нужно хранить уникальное соответствие между двумя множествами значений. Их помещают в ключ, и структура проверяет, чтобы ключ не повторялся.

Частный случай map — это hash-map, или хэш-таблица. В ней есть ключи и значения, а для их реализации добавляются индексы. Специальная хэш-функция позволяет по ключу вычислить индекс, чтобы найти нужные данные.

Временная сложность хэш-таблицы

| Алгоритм | Среднее значение | Худший случай |
|----------|------------------|---------------|
| Space    | O(n)             | O(n)          |
| Search   | O(1)             | O(n)          |
| Insert   | O(1)             | O(n)          |
| Delete   | O(1)             | O(n)          |

## Двоичное дерево поиска (Binary search tree)

Дерево — это структура, данные в которой лежат в узлах. У каждого узла могут быть один или несколько дочерних и только один родитель, то есть они расходятся, как ветви дерева.

Деревья бывают разных типов, но наиболее распространены двоичные деревья поиска. У них есть следующие особенности:
- У каждого узла не больше двух дочерних.
- Если новое значение меньше, оно становится левым дочерним либо дочерним левого дочернего.
- Если значение больше, оно становится правым дочерним или дочерним правого дочернего.

Как применяют двоичные деревья:
- Для быстрого поиска данных.
- Для хранения данных в отсортированном виде с возможностью быстро их добавлять и удалять.

Временная сложность

| Алгоритм | Среднее значение | Худший случай |
|----------|------------------|---------------|
| Space    | O(n)             | O(n)          |
| Search   | O(log n)         | O(n)          |
| Insert   | O(log n)         | O(n)          |
| Delete   | O(log n)         | O(n)          |

## Граф (Graph)

Граф — это более общий случай дерева. Иногда деревья называют ациклическими графами. Отличий у этих структур данных два:
- В графе возможны циклы, то есть «ребёнок» может быть «родителем» для того же элемента.
- Рёбра тоже могут нести смысловую нагрузку, то есть нужно сохранять их значения.

Графы бывают ориентированные и неориентированные. У первых рёбра между узлами имеют направление, так что порядок элементов важен. У вторых направлений нет, и элементы можно читать и обходить в любом порядке.

Графы часто представляют в виде матрицы смежности.

Как применяют графы:
- Для хранения информации, связанной друг с другом сложными соотношениями.
- Для анализа соотносящейся друг с другом информации.
- Для построения маршрута из точки А в точку Б.
