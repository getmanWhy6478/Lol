# Рассчётная работа 
## Вариант 4.16

**Базовые определения:**

**Граф** – это топологичекая модель, которая состоит из множества вершин и множества соединяющих их рёбер. При этом значение имеет только сам факт, какая вершина с какой соединена.

**Инцидентность** (смежность) – отношение между двумя вершинами, в котором существует ребро их соединяющее.

**Концевые вершины графа** - вершины, соединяющие данное множество ребер.

**Эйлеров обход** - рекурсивный алгоритм обхода графа, начинающий в произвольной вершине и рекурсивно обходящий весь граф, посещая каждую вершину ровно один раз.

**Подграф** - это часть графа, в которой мы берем некоторые его вершины и ребра. Другими словами, граф H является подграфом графа G, если вершины и ребра H являются подмножеством вершин и ребер G.

**Компонента сильной связности** - компонента, в которой все вершины сильно связаны, а между вершинами разных компонент сильной связности нет.

**Связанные сильно вершины** - вершины такие, что существует путь из одной в другую и наоборот.

**Граф конденсации** - граф, в котором каждая компнента сильной связности сжаты до одной вершины.

**Топологическая сортировка** - порядок вершин, в котором все рёбра графа ведут из более ранней вершины в более позднюю.

## Цель данной работы:

Реализовать один из алгоритмов для построения графа конденсации для орграфа, с использованием языка программирования С++
Исследовать работу алгоритма и описать её

## Описание алгоритма:
**Входные данные:**

На вход алгоритму подаётся ориентриованный граф

## Исполнение алгоритма:
Пусть дан граф G (см. рис. 1):


![начало](https://github.com/user-attachments/assets/3edf61af-ae14-42f3-8174-2a9a06265d6e)

Начнём Эйлеров обход с вершины 1. В случае, если из вершины нельзя будет попасть в другую ранее не посещённую вершину, запишем её в список и вернёмся к вершине, из которой мы пришли в данную.

В данном случае в результате получим такой список: {6, 7, 9, 10, 8, 5, 11, 4, 3, 2, 1}

![обход](https://github.com/user-attachments/assets/b8594d5c-82ac-48b5-98c2-20bf7e31c9d8)

(В прямоугольниках подписан порядок прохождения вершин во время обхода)

После этого развернём рёбра данного графа. В итоге получим:


![рев](https://github.com/user-attachments/assets/8d300d79-33ad-48af-a7d0-dbc5e2c5411c)

После этого будем выбирать последнюю вершину с конца списка сортировки и делать Эйлеров обход начиная с него, при этом удаляя эту вершину из списка сортировки. В случае, если из вершины можно попасть в какую-то другую вершину, данная вершина добавляется в компоненту сильной связности. Как только это невозможно, компонента добавляется в список компонент графа.
## Завершение работы
Продолжая таким образом, в итоге получим плоскую укладку исходного графа G(см. рис. 8).

<image src="/Снимок экрана 2024-12-10 221216.png" alt="Рисунок 8">

# Заключение
В результате проведённой работы удалось:

1. Изучить материалы по методам нахождения графа конденсации
2. Выбрать алгоритм решения данной задачи и реализовать на языке С++
3. Выполнить иследование выбранного алгоритма на производительность и эффективность

