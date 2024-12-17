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

На вход алгоритму подаются ориентриованный граф

## Исполнение алгоритма:
Пусть дан граф G (см. рис. 1):


![начало](https://github.com/user-attachments/assets/3edf61af-ae14-42f3-8174-2a9a06265d6e)

Начнём Эйлеров обход с вершины 1. В случае, если из вершины нельзя будет попасть в другую ранее не посещённую вершину, запишем её в список и вернёмся к вершине, из которой мы пришли в данную.

В данном случае в результате получим такой список: {6, 7, 9, 10, 8, 5, 11, 4, 3, 2, 1}

![начало](https://github.com/user-attachments/assets/53d612bc-75e4-4435-b06e-6dd58981dc30)

(В прямоугольниках подписан порядок прохождения вершин во время обхода)

После этого развернём рёбра данного графа. В итоге получим:


![рев](https://github.com/user-attachments/assets/968ae231-93f5-419b-85b3-09791774de4b)

Уже уложенную часть исходного графа будем обозначать как G′, тогда после первого шага G′ представляет собой цикл {1, 2, 3, 4, 5, 6}.

На каждом шаге будем строить множество сегментов. Каждый сегмент S относительно уже построенного графа G′ представляет собой одно из двух:

ребро, оба конца которого принадлежат G′, но само оно не принадлежит G′;
связную компоненту графа G – G′, дополненную всеми ребрами графа G, один из концов которых принадлежит связной компоненте, а второй из графа G′.
Вершины, которые одновременно принадлежат G′ и какому-то сегменту, назовем контактными вершинами. Для нашего примера сегменты изображены на рис. 3. Контактные вершины обведены в квадрат.

<image src="/Снимок экрана 2024-12-10 220355.png" alt="Рисунок 3">

Если все контактные вершины сегмента S имеют номера вершин какой-то грани Г, то мы будем говорить, что грань Г вмещает этот сегмент, в этом случае будем использовать следующее обозначение: S Г. Однако, может быть так, что не одна грань вмещает в себя сегмент S, а несколько. Множество таких граней обозначим Г(S), а их число |Г(S)|.

**Общий шаг**
Выделяются все сегменты Si и определяются числа |Г(Si)|. Если хоть одно из них равно 0, то граф не планарен, конец. Иначе, выбираем сегмент, для которого число |Г(S)| минимально, или любой из них, если таких сегментов несколько. В этом сегменте найдем произвольную цепь между двумя контактными вершинами и уложим ее в любую из граней множества Г(S). При этом данная грань разобьется на две. Уже уложенная часть графа G’ после укладки цепи увеличится, а сегмент, из которого вынута цепь, исчезнет или развалится на меньшие с новыми контактными вершинами, ведущими к вершинам G′.

В результате повторения общего шага будет либо получена плоская укладка, когда множество сегментов станет пустым, либо будет получено, что граф G не является планарным.

Вернемся к нашему примеру. Пока для любого i: Si {Г1, Г2}, |Г(Si)| = 2. Поэтому возьмем первый по номеру сегмент Si и в нем цепь {1, 4}; вставим эту цепь в грань Г2. После укладки цепи G’ увеличится и произойдут изменения в структуре сегментов (см. рис. 4, 5).

<image src="/Снимок экрана 2024-12-10 221005.png" alt="Рисунок 4">

<image src="/Снимок экрана 2024-12-10 221024.png" alt="Рисунок 5">

Определим, какие грани вмещают новые сегменты. Теперь сегменты S1 и S3 можно уложить только в одну грань Г1, в то время как сегменты S2 и S4 можно уложить в две грани (для S2 это грани Г1 и Г2, для S4 - Г1 и Г3). Поэтому берем S1. Возьмем в нем цепь {2, 5} и уложим ее в Г1. Получим увеличенный граф G′ и уменьшенную систему сегментов (см. рис. 6, 7).

<image src="/Снимок экрана 2024-12-10 221044.png" alt="Рисунок 6">

<image src="/Снимок экрана 2024-12-10 221156.png" alt="Рисунок 7">

## Завершение работы
Продолжая таким образом, в итоге получим плоскую укладку исходного графа G(см. рис. 8).

<image src="/Снимок экрана 2024-12-10 221216.png" alt="Рисунок 8">

# Заключение
В результате проведённой работы удалось:

1. Изучить материалы по методам нахождения графа конденсации
2. Выбрать алгоритм решения данной задачи и реализовать на языке С++
3. Выполнить иследование выбранного алгоритма на производительность и эффективность

