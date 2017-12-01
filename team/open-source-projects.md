# Наши проекты

Большую часть своего времени мы работаем над приложениями для различных подразделений группы компаний RAMBLER&Co. Но, кроме этого, мы стараемся выделять время и силы на создание и развитие собственных проектов.

- [Рамблер/IT](#Рамблерit)
- [Prokrut](#prokrut)
- [Генерамба](#Генерамба)
- [The Book of VIPER](#the-book-of-viper)
- [ViperMcFlurry](#vipermcflurry)
- [RamblerTyphoonUtils](#ramblertyphoonutils)
- [RamblerSegues](#ramblersegues)
- [Dashramba](#dashramba)
- [Ramb-n-roll](#ramb-n-roll)
- [Fastlane flows](#fastlane-flows)
- [Rambobot](#rambobot)
- [RamblerAppDelegateProxy](#ramblerappdelegateproxy)
- [RambagramPageControl](#rambagrampagecontrol)
- [RamblerSpotlight](#ramblerspotlight)

### [Рамблер/IT](https://github.com/rambler-digital-solutions/rambler-it-ios)
Приложение предназначено для слежения за конференциями, проходящими в RAMBLER&Co, просмотра списка их докладчиков, записей выступлений и слайдов.

Технические особенности. 

- Используется 3-tier архитектура. Приложение разбито на 3 слоя: presentation, service, core.
- Presentation слой написан с использованием VIPER.
- Core-слой написан с использованием compound-операций.

#### Цели
- Cлужить демонстрацией используемых нами архитектурных подходов и принципов в Objective-C проектах.

#### Состояние проекта
Приложение находится в стадии поддержки.

#### Дополнительные ссылки
- [Задачи текущей версии](https://github.com/rambler-digital-solutions/rambler-it-ios/issues?q=is%3Aopen+is%3Aissue+milestone%3A1.3). 
- [Основные разработчики](https://github.com/rambler-digital-solutions/rambler-it-ios/graphs/contributors). 

### [Prokrut](https://github.com/strongself/Prokrut)
Часть нашей команды очень любит кикер. И меряться очками. Любит настолько, что даже написала для этого отдельное приложение, с помощью которого ведется статистика результатов игроков. Сезоны, графики, ачивки, пуши - вот это все есть в приложении.

#### Цели
- Предоставлять максимально удобный сервис для командной игры в кикер.

#### Состояние проекта
Проект заморожен.

#### Дополнительные ссылки
- [Доска проекта](https://github.com/strongself/Prokrut/projects/1). 
- [Основные разработчики](https://github.com/strongself/Prokrut/graphs/contributors). 

### [Генерамба](https://github.com/rambler-digital-solutions/Generamba)
В один исторический момент Xcode'овские шаблоны показались нам ограниченными и неудобными. Мы написали свой велосипед, который, конечно же, абсолютно идеален. Генерамба умеет добавлять файлы и в папки, и в .xcodeproj, работает с liquid шаблонами, поддерживает Cocoapods - и кучу чего еще. Подробнее можно почитать в [обзорной статье](http://etolstoy.com/2016/02/10/generamba/).

#### Цели
- Автоматизировать рутинные задачи по генерации и предзаполнению новых файлов.

#### Состояние проекта
Проект заморожен.

#### Дополнительные ссылки
- [Задачи версии 2.0](https://github.com/rambler-digital-solutions/Generamba/issues?q=is%3Aissue+is%3Aopen+milestone%3Av.2.0-alpha). 
- [Основные разработчики](https://github.com/rambler-digital-solutions/Generamba/graphs/contributors). 
- [Каталог шаблонов](https://github.com/rambler-digital-solutions/generamba-catalog). 

### [The Book of VIPER](https://github.com/rambler-digital-solutions/The-Book-of-VIPER)
В качестве основного подхода к архитектуре Presentation-слоя наших приложений мы используем архитектуру VIPER. ЗЗа долгое время работы мы собрали целую базу знаний, инструкций и практик по работе с ним и дали этой коллекции гордое название "Книга VIPER".

#### Цели
- Предоставлять максимально полную информацию об использовании VIPER.
- Оформить проект в виде законченного e-book издания.

#### Состояние проекта
Базовое наполнение готово, требуется перевод на английский язык.

#### Дополнительные ссылки
- [Задачи по переводу проекта](https://github.com/strongself/The-Book-of-VIPER/issues?q=is%3Aopen+is%3Aissue+label%3Aenglish). 
- [Основные разработчики](https://github.com/rambler-digital-solutions/The-Book-of-VIPER/graphs/contributors). 

### [ViperMcFlurry](https://github.com/rambler-digital-solutions/ViperMcFlurry)
При адаптации VIPER в своем проекте iOS-разработчики всегда задают два вопроса: как передавать данные между модулями и как создать новый модуль. Эта библиотека решает обе задачи. 

#### Цели
- Упростить реализацию VIPER в iOS-приложениях.

#### Состояние проекта
Проект готов.

#### Дополнительные ссылки
- [Основные разработчики](https://github.com/rambler-digital-solutions/ViperMcFlurry/graphs/contributors).

### [RamblerTyphoonUtils](https://github.com/rambler-digital-solutions/RamblerTyphoonUtils)
Для маленьких и средних проектов на Objective-C фреймворк [Typhoon](https://github.com/appsquickly/Typhoon) - идеальное решение для DI. А чтобы интеграция Typhoon в проект на VIPER занимала всего пару шагов, был создан этот проект. 

#### Цели
- Упростить реализацию VIPER в iOS-приложениях.

#### Состояние проекта
Проект готов.

#### Дополнительные ссылки
- [Основные разработчики](https://github.com/rambler-digital-solutions/RamblerTyphoonUtils/graphs/contributors).

### [RamblerSegues](https://github.com/rambler-digital-solutions/RamblerSegues)
Когда-то работа с переходами между экранами, верстка которых находится в *.storyboard-файлах, была нелогичной, требовала значительных усилий со стороны разработчиков. Чтобы решить эту проблему, мы написали свои вспомогательные segue и запаковали их в opensoure-библиотеку.  

#### Цели
- Упростить переходы между экранами приложений.

#### Состояние проекта
Проект готов.

#### Дополнительные ссылки
- [Основные разработчики](https://github.com/rambler-digital-solutions/RamblerSegues/graphs/contributors).

### [Dashramba](https://github.com/rambler-digital-solutions/dashramba)
Рабочих проектов у нас много, статистики по каждому из них - еще больше, но разбросана она по десятку разных сервисов: Fabric, Jenkins, AppStore, GitLab, Upsource. Для агрегирования этой информации мы решили написать dashboard на базе чудесного проекта [Dashing](http://dashing.io/).

#### Цели
- Автоматизация сбора метрик всех проектов. 

#### Состояние проекта
Проект медленно развивается.

#### Дополнительные ссылки
- [Текущий список задач](https://github.com/rambler-digital-solutions/dashramba/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20). 
- [Основные разработчики](https://github.com/rambler-digital-solutions/dashramba/graphs/contributors). 

### [Ramb-n-roll](https://github.com/rambler-digital-solutions/rambnroll)
Процесс доставки сборок до тестировщиков и менеджеров всегда требует особого отношения. Чтобы получение тестового билда было максимально быстрым, мы стартовали разработку нашего собственного инструмента. 

#### Цели
- Создать универсальный инструмент для взаимодействия с CI-системами. 
- Создать хранилище тестовых сборок. 

#### Состояние проекта
Проект готовиться к выходу в open-source.

### [Fastlane flows](https://github.com/rambler-digital-solutions/fastlane-flows)
Сборка и подпись приложений - нетривиальная задача. Феликсу Краузе как-то надоело заниматься этим вручную, и он начал проект [fastlane](https://fastlane.tools/), который в настоящее время считается стандартом при распространении приложений: у каждой команды есть свои, упрощающие жизнь, lanes для запуска fastlane. "Мы не хуже", - подумал кто-то из нас и начал этот проект. 

#### Цели
- Создать удобные и гибкие lanes для fastlane. 

#### Состояние проекта
Проект развивается параллельно с [Ramb-n-roll](#ramb-n-roll).

#### Дополнительные ссылки
- [Текущий список задач](https://github.com/rambler-digital-solutions/fastlane-flows/issues). 
- [Основные разработчики](https://github.com/rambler-digital-solutions/fastlane-flows/graphs/contributors). 

### [Rambobot](https://github.com/strongself/rambobot)
На [Rambler.iOS](/team/meetups/rambler-ios/about.md) мы регулярно проводим викторины. Но в какой-то момент нам надоело вручную подсчитывать ответы пользователей, отслеживать, кто из них поднял руку первым. И, как настоящие инженеры, мы написали свое решение. 

#### Цели
- Упростить проведение викторин в рамках конференций. 

#### Состояние проекта
Проект не развивается, но ему требуется хороший рефакторинг.

#### Дополниниельные ссылки
- [Текущие задачи](https://github.com/strongself/rambobot/issues). 
- [Основные разработчики](https://github.com/strongself/rambobot/graphs/contributors). 

### [RamblerAppDelegateProxy](https://github.com/strongself/RamblerAppDelegateProxy)
Помимо больших проектов у нас есть и множество вспомогательных. Один из них - это RamblerAppDelegateProxy. Эта библиотека создана только с одной целью - решить проблему массивного AppDelegate. 

#### Цели
- Устранение массивного AppDelegate. 

#### Состояние проекта
Проект готов.

#### Дополнительные ссылки
- [Основные разработчики](https://github.com/strongself/RamblerAppDelegateProxy/graphs/contributors). 

### [RambagramPageControl](https://github.com/rambler-digital-solutions/RambagramPageControl)
Если хотите добавить в свой проект красивый и удобный page control, то этот проект специально для вас. 

#### Цели
- Создать page control не хуже, чем в Instagram. 

#### Состояние проекта
Проект готов.

#### Дополнительные ссылки
- [Основные разработчики](https://github.com/rambler-digital-solutions/RambagramPageControl/graphs/contributors). 

### [RamblerSpotlight](https://github.com/strongself/RamblerSpotlight)
В iOS 9 Apple представила фреймворк [CoreSpotlight](https://developer.apple.com/documentation/corespotlight). Используя его, вы легко можете индексировать контент своих приложений в системе и упростить взаимодействие между приложениями. Но, к сожалению, взаимодействие с фреймворком не такое простое, как может показаться пользователю. Чтобы придать ему легкости и изящества, мы разработали свое решение, о котором даже написали на [Хабре](https://habrahabr.ru/company/rambler-co/blog/268257/). 

#### Цели
- Упростить и стандартизовать работу с CoreSpotlight. 

#### Состояние проекта
Проект готов.

#### Дополнительные ссылки
- [Основные разработчики](https://github.com/strongself/RamblerSpotlight/graphs/contributors). 
