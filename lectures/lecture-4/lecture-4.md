---
author: 𝕭𝖊𝖎𝖅𝖊𝖗𝖔
title: Области видимости
<!-- date: January 28, 2018 -->
---

## Вложенные функции

Вспомним реализацию функции `sqrt`:

```scala
def sqrtIter(guess: Double, x: Double): Double =
  if (isGoodEnough(guess, x)) guess
  else sqrtIter(improve(guess, x), x)

def improve(guess: Double, x: Double) =
  (guess + x / guess) / 2

def isGoodEnough(guess: Double, x: Double) =
  abs(square(guess) - x) < 0.001

def sqrt(x: Double) = sqrtIter(1.0, x)
```

## Вложенные функции

Разбиение большой задачи на множество маленьких функций является хорошей практикой в функциональном программировании.

Но функции вроде `improve`, `isGoodEnough` и `sqrtIter` нужны только для реализации `sqrt` и пользователь не должен обращаться к ним напрямую.

## Вложенные функции

Чтобы не загрязнять пространство имён можно поместить их внутрь `sqrt`:
```scala
def sqrt(x: Double) = {
  def sqrtIter(guess: Double, x: Double): Double =
    if (isGoodEnough(guess, x)) guess
    else sqrtIter(improve(guess, x), x)

  def improve(guess: Double, x: Double) =
    (guess + x / guess) / 2

  def isGoodEnough(guess: Double, x: Double) =
    abs(square(guess) - x) < 0.001

  sqrtIter(1.0, x)
}
```
