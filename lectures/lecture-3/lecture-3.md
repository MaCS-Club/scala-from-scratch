---
author: 𝕭𝖊𝖎𝖅𝖊𝖗𝖔
title: Рекурсия
<!-- date: January 28, 2018 -->
---

## Условные выражения

Для выбора между двумя альтернативами в Scala есть условное выражение `if-else`

```scala
def abs(x: Double) = if (x >= 0) x else -x
```

## Булевые выражения

Булевые выражения могут состоять из

```scala
true  false      // Константы
!b               // Отрицание
b && b           // Конъюнкция
b || b           // Дизъюнкция
```

и из обычных операций сравнения

```scala
e <= e, e >= e, e < e, e > e, e == e, e != e
```

## Редукция булевых выражений

Правила редукции для булевых выражений(`e` произвольное):

```scala
!true --> false
!false --> true
true && e --> e
false && e --> false
true || e --> true
false || e --> e
```

## Редукция булевых выражений

Обратите внимание, что `&&` и `||` не всегда нужен их правый операнд для вычисления.

Говрят что такие выражения вычисляются по сокращённой схеме (short-circuit evaluation).

## Вычисление квадратного корня

Определим метод

```scala
/** Calculates the square root of parameter x */
def sqrt(x: Double): Double = ...
```

Классический способ его реализации это последовательные приближения с использованием метода Ньютона.

## Метод Ньютона

Для вычисления `sqrt(x)`:

* Стартуем с начальной оценки `y`(возьмём `y = 1`)
* Повторяясь улучшаем оценку беря среднее значение `y` и `x / y`

## Метод Ньютона

Пример:

| Оценка | Частное               | Среднее |
|--------|-----------------------|---------|
| 1      | 2 / 1 = 2             | 1.5     |
| 1.5    | 2 / 1.5 = 1.333       | 1.4167  |
| 1.4167 | 2 / 1.4167 = 1.4118   | 1.4142  |
| 1.4142 | ...                   | ...     |

## Реализация на Scala

Сначала мы определим метод который вычисляет одну итерацию:

```scala
def sqrtIter(guess: Double, x: Double): Double =
  if (isGoodEnough(guess, x)) guess
  else sqrtIter(improve(guess, x), x)
```

##

Обратите внимание, что `sqrtIter` рекурсивна т.к. вызывает сама себя.

Для рекурсивных функций в Scala необходимо явно указывать тип возвращаемого значения.

Для не рекурсивных функций это не обязательно.

## Реализация на Scala

Затем мы определим метод `improve` для улучшения оценки и терминирующее условие `isGoodEnough`:

```scala
def improve(guess: Double, x: Double) =
  (guess + x / guess) / 2

def isGoodEnough(guess: Double, x: Double) =
  abs(guess * guess - x) < 0.001
```

## Реализация на Scala

Ну и наконец определим функцию `sqrt`:

```scala
def sqrt(x: Double) = sqrtIter(1.0, x)
```

## Применение рекурсивных функций

Давайте сравним этапы вычисления двух рекурсивных функций.

##

Первой функцией будет `gcd` вычисляющей наибольший общий делитель двух чисел по алгоритму Евклида.

```scala
def gcd(a: Int, b: Int): Int =
  if (b == 0) a else gcd(b, a % b)
```

## Вычисление gcd

```scala
gcd(14, 21)
if (21 == 0) 14 else gcd(21, 14 % 21)
if (false) 14 else gcd(21, 14 % 21)
gcd(21, 14 % 21)
gcd(21, 14)
if (14 == 0) 21 else gcd(14, 21 % 14)
if (false) 21 else gcd(14, 21 % 14)
gcd(14, 7)
gcd(7, 14 % 7)
gcd(7, 0)
if (0 == 0) 7 else gcd(0, 7 % 0)
if (true) 7 else gcd(0, 7 % 0)
7
```

##

Второй функцией будет `factorial`:

```scala
def factorial(n: Int): Int =
  if (n == 0) 1 else n * factorial(n - 1)
```

## Вычисление factorial

```scala
factorial(4)
if (4 == 0) 1 else 4 * factorial(4 - 1)
4 * factorial(3)
4 * (3 * factorial(2))
4 * (3 * (2 * factorial(1)))
4 * (3 * (2 * (1 * factorial(0)))
4 * (3 * (2 * (1 * 1)))
24
```

##

Различие в вычислении этих функций в том, что `gcd` просто вызывает себя несколько раз и потом завершается, а `factorial` на каждом шаге добавляет элемент к выражению которое становится всё больше и только потом редуцируется к результату.

##

Происходит это потому, что `gcd` вызывает себя последним действием, а `factorial` последнием действием применяет умножение.

```scala
def gcd(a: Int, b: Int): Int =
  if (b == 0) a else gcd(b, a % b)

def factorial(n: Int): Int =
  if (n == 0) 1 else n * factorial(n - 1)
```

## Хвостовая рекурсия

Разница в применении данных функций так же влияет на их вычисление компьютером.

Если есть рекурсивная функция вызывающая себя последним действием, то можно переиспользовать выделенное для неё место на стеке.

Это называется хвостовой рекурсией.

## Хвостовая рекурсия

Пользуясь этой хитростью можно добиться того, чтобы функции использующие хвостовую рекурсию использовали для своего вычисления константное место на стеке.

## Хвостовая рекурсия в Scala

Можно потребовать, чтобы функция использовала хвостовую рекурсию с помощью аннотации `@tailrec`:

```scala
@tailrec
def gcd(a: Int, b: Int): Int = …
```

Если данная аннотация присутствует, но реализация функции не хвостоворекурсивная, то вы получите ошибку.