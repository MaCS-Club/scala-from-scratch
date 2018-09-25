---
author: 𝕭𝖊𝖎𝖅𝖊𝖗𝖔
title: Введение
<!-- date: January 28, 2018 -->
---

## Что такое Scala?

Scala(SCAlable LАnguage) — мультипарадигмальный язык программирования, спроектированный кратким и типобезопасным для простого и быстрого создания компонентного программного обеспечения, сочетающий возможности функционального и объектно-ориентированного программирования.

## Почему Scala?

* Выразительный и гибкий
* Является языком общего назначения
* Активно развивается
* Есть REPL(Read–eval–print loop)
* Программы запускаются на JVM(Java Virtual Machine)
* Совместимость с Java
* Есть возможность компиляции в JavaScript

## Компании ведущие разработку на Scala

Twitter, LinkedIn, Apple, Foursquare, The Guardian, Coursera, Quora, Yandex, Тинькофф, Luxoft, Verizon, Airbnb, Walmart Canada, Google

## Установка

* Установить [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* Перейти на сайт [scala-lang.org](https://www.scala-lang.org)
* Нажать на кнопку *DOWNLOAD*
* Выбрать установку *INTELLIJ IDEA* и следовать инструкции
* При установке необходимо выполнить установку плагина для Scala

## Создание проекта

* Открыть IDEA и нажать _Create new project_
* Выбрать вкладку Scala и выбрать _Sbt project_
* Заполнить необходимые поля

## Файлы и директории проекта

* `.idea` техническая папка Intellij IDEA
* `project` содержит вспомогательные объекты для `build.sbt` и плагины для `SBT`
* `src` содержит файлы с исходным кодом
* `build.sbt` содержит информацию необходимую для сборки проекта(название, версии, зависимости)

## Hello, world!

Теперь создадим простую программу выводящую надпись "Hello, world!" на экран.

Для этого в папке `src/main/scala` создадим файл `HelloWorld.scala` со следующим текстом:

(при необходимости нажимаем _Setup Scala SDK_ и выбираем самую новую версию библиотеки)

## Hello, world!!

```scala
object HelloWorld extends App {
  println("Hello, world!")
}
```

## Hello, world!!!

Для компиляции и выполнения написаного кода на вкладке `sbt shell`(находится в левом нижнем углу) необходимо выполнить команду `run`.

## Список литературы

* «Scala для нетерпеливых», Кей Хорстман
* «Programming in Scala», Martin Odersky
* «Scala by examples», Martin Odersky
* Специализация «Functional programming in Scala» на Coursera
