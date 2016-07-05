### Настройка CI на Jenkins

1. Создайте новый проект: на экране Dashboard нажмите на кнопку *New Item*.
  1. Введите название проекта. Название проекта должно состоять из трех частей: `Company.ProjectName.Department`. Например, *Rambler.Mail.iOS*.
  2. Выберите тип проекта: *Copy from existing project*
  3. Выберите проект для копирования: *iOS-ci-config-project*
2. На экране настроек проекта
  1. Введите описание проекта.
  2. Подключите репозиторий проекта в разделе Source Code Management:
      1. Введите HTTPS-адрес репозитория в Repository URL. Например: `https://***REMOVED***/mobile-dev/livejournal-ios.git`.
      2. Для того, чтобы проект собрался, нужно в Xcode зайти в *Product -> Scheme -> Manage Schemes* и сделать следующее:
          1. Для тестового target в графе Container выбрать workspace
          2. Для тестового target включить чекбокс shared
3. Настройка [GitLab](https://***REMOVED***
).
  1. В настройках проекта в разделе *Web Hooks* добавьте новый хук.
  2. Введите url проекта на jenkins. Например, [LiveJournal](http://***REMOVED***). Обратите внимание, что в качестве URL используется именно `http://***REMOVED***/project/ID_ПРОЕКТА`.
  3. В качестве токена добавьте любую строку.
4. Настройка сборки
  1. Настройте [*fastlane*](/processes/continuous-delivery/simple-setup.md#Шаг-4-Базовая-настройка-fastlane).
  2. Создайте и заполните Scanfile по [образцу](/processes/continuous-integration/scanfile-example.md).
  3. Добавьте шаг сборки "Выполнить команду шел".
  4. В появившемся поле вставьте скрипт.

#### Скрипт

```sh
#!/bin/bash -l

fastlane build_test
```
