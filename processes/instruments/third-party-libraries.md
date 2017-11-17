### Используемые библиотеки

Мы за использование сторонних библиотек. Изобретать свои велосипеды, если задача уже была качественно решена кем-то еще - как минимум бессмысленно.

Перед тем, как добавить в проект еще одну зависимость, мысленно пройдитесь по короткому чек-листу:

- Есть ли среди стандартного стека используемых в Rambler&Co библиотек то, что может решить вашу задачу?
- Достаточно ли существенна текущая задача, чтобы внедрять в проект новый компонент, с учетом времени на инспекцию его кода?
- Насколько качественно написана библиотека?

Эти простые вопросы помогут поддерживать общее количество зависимостей в разумных пределах и не тащить в проект бесполезные зависимости.

#### Стандартный стек используемых библиотек

- **[Typhoon](https://github.com/appsquickly/Typhoon)** - DI контейнер.
- **[MagicalRecord](https://github.com/magicalpanda/MagicalRecord)** - реализация ActiveRecord для CoreData.
- **[Nimbus/Models](http://nimbuskit.info/)** - реализация datasources для работы с UITableView/UICollectionView.
- **[CocoaLumberjack](https://github.com/CocoaLumberjack/CocoaLumberjack)** - библиотека для логирования
- **[SDWebImage](https://github.com/rs/SDWebImage)** - загрузка web изображений.
- **[RestKit/Mapping](https://github.com/RestKit/RestKit)** - библиотека для маппинга.
- **[EasyMapping](https://github.com/lucasmedeirosleite/EasyMapping)** - библиотека для маппинга.
- **[PureLayout](https://github.com/PureLayout/PureLayout)** - работа с autolayout в коде.
- **[OCMock](http://ocmock.org/)** - мокирование объектов.
- **[OHHTTPStubs](https://github.com/AliSoftware/OHHTTPStubs)** - работа с сетевыми стабами.

Отдельное важное уточнение - для написания юнит-тестов используется ванильный **XCTest**.