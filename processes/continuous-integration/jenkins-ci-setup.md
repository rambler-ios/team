### Настройка CI на Jenkins


1. Создайте новый проект: на экране Dashboard нажмите на кнопку *New Item*.
  1. Введите название проекта. Название проекта должно состоять из трех частей: `Company.ProjectName.Department`. Например, *Rambler.Mail.iOS*.
  2. Выберите тип проекта: *Copy from existing project*
  3. Выберите проект для копирования: *iOS-ci-config-project*
2. На экране настроек проекта
  1. Введите описание проекта.
  2. Подключите репозиторий проекта в разделе Source Code Management:
      1. Введите HTTPS-адрес репозитория в Repository URL. Например: `https://gitlab.rambler.ru/mobile-dev/livejournal-ios.git`.
      2. Для того, чтобы проект собрался, нужно в Xcode зайти в *Product -> Scheme -> Manage Schemes* и сделать следующее:
          1. Для тестового target в графе Container выбрать workspace
          2. Для тестового target включить чекбокс shared
3. Настройка [GitLab](https://gitlab.rambler.ru
).
  1. В настройках проекта в разделе *Services* включите *GitLab CI*.
  2. В настройках GitLab CI проекта введите любой токен и url проекта на jenkins. Например, [LiveJournal](http://ci.dev.rambler.ru/jenkins/project/Sup.LiveJournal.iOS).
