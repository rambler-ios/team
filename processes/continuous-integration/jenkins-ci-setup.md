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
  2. Введите url проекта на jenkins. Например, [LiveJournal](http://***REMOVED***).
  3. В качестве токена добавьте любую строку.
4. Настройка build.sh
  1. Добавьте пустой файл *build.sh* в корневую папку проекта.
  2. Настройте переменные `workspace`, `scheme`, `sourceDir=`.
  3. Выполните команду в консоли в папке проекта: `chmod +x build.sh`.

#### Пример скрипта

```sh
#!/bin/bash -l
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
export LC_CTYPE=en_US.UTF-8
 
#Configuration
workspace=LiveJournal
scheme=LiveJournal
sourceDir=LiveJournal
reportsDir=build/reports
 
#Fail immediately if a task fails
set -e
set -o pipefail
 
#Clean
rm -fr ~/Library/Developer/Xcode/DerivedData
rm -fr ./build
#Compile, run tests
iosVersion='9.1'
xcodebuild test -workspace ${workspace}.xcworkspace -scheme ${scheme} -configuration Debug \
-destination "platform=iOS Simulator,name=iPhone 5s,OS=${iosVersion}" ONLY_ACTIVE_ARCH=YES | xcpretty -c --report junit
```
