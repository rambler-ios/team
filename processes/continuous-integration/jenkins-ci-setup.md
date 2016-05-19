### Настройка CI на Jenkins


1. Создайте новый проект: на экране Dashboard нажмите на кнопку *New Item*.
  1. Введите название проекта. Название проекта должно состоять из трех частей: `Company.ProjectName.Department`. Например, *Rambler.Mail.iOS*.
  2. Выберите тип проекта: *Freestyle project*
2. На экране настроек проекта
  1. Введите описание проекта.
  2. Настройте уведомления Slack в разделе Slack Notifications.
  3. Введите label сборщика проектов в разделе *Advanced Project Options / Restrict where this project can be run*: `macosx`.
  4. Подключите репозиторий проекта в разделе Source Code Management:
      1. Выберите Git
      2. Введите HTTPS-адрес репозитория в Repository URL. Например: `https://***REMOVED***/mobile-dev/livejournal-ios.git`.
      3. Выберите в Credentials пользователь jenkins для https://***REMOVED*** - jenkins.ci
  5. Введите бранчи для сборки в *Branches to build*. Для обычных проектов оставьте поле пустым.
  6. Введите периодичность проверки репозитория в *Build Triggers*.
      1. Для сборки проекта по пушу выберите Build when a change is pushed to GitLab. 
          1. Убедитесь, что *Build on Push Events* включено.
          2. Выберите бранчи *develop* и *master* в *Filter branch*. Если список бранчей пуст, убедитесь что в пункте `2.4.2` указали правильный адрес репозитория, сохраните настройки и перегрузите страницу.
  7. Добавьте build step *Xcode* и заполните настройки:
      1. Убедитесь, что включена настройка Clean test reports.
      2. Для тестирования на симуляторе необходимо настроить следующие поля:
          1. *Xcode Schema File* - укажите свою тестовую схему 
          2. *SDK* - введите `iphonesimulator`
          3. *Custom xcodebuild arguments* - введите  -`destination 'platform=iOS Simulator,name=iPhone 5'  test`
          4. Укажите *Xcode Workspace File*
      3. Для того, чтобы проект собрался, нужно в Xcode зайти в *Product -> Scheme -> Manage Schemes* и сделать следующее:
          1. Для тестового target в графе Container выбрать workspace
          2. Для тестового target включить чекбокс shared
  8. Настройте Post-build Actions:
      1. Добавьте *Slack notifications*
3. Настройка [GitLab](https://***REMOVED***
).
  1. В настройках проекта в разделе *Services* включите *GitLab CI*.
  2. В настройках GitLab CI проекта введите любой токен и url проекта на jenkins. Например, [LiveJournal](http://***REMOVED***).