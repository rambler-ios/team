### Continuous Delivery Troubleshooting

#### Часто встречающиеся проблемы

**Q:** No value found for username.
  
**A:** Скорее всего вы указали некорректные названия лейнов в Appfile. Другой вариант - убедитесь, что в этом файле проставлены правильные кавычки вокруг bundle id - TextEdit, например, ставит неправильные кавычки, от которых сборка ломается.
  
**Q:** Could not find fastlane in current directory. Would you like to set it up? (y/n)

**A:** Нужно убедиться, что в корневой папке проекта создана папка fastlane со всем необходимым содержимым. Также нужно удостовериться, что внесенные при настройке сборок изменения были запушены на Gitlab.

**Q:** Could not find App with App Identifier *%ВАШ_BUNDLE_ID%.enterprise*.

**A:** Следует убедиться, что приложение с соответствующим bundle id создано в enterprise аккаунте Рамблера.

**Q:** Code Sign error: No matching provisioning profiles found: No provisioning profiles with a valid signing identity (i.e. certificate and private key pair) matching the bundle identifier *%ВАШ_BUNDLE_ID%.enterprise* were found

**A:** Следует убедиться, что в основном таргете проекта во вкладке General в пункте Team выбрано None.

**Q:** ERROR: Step ‘Publish JUnit test result report’ failed: No test report files were found. Configuration error?

**A:** В Jenkins в настройках проекта в Post-build actions следует удалить этап Publish JUnit test result report, для ночных сборок он не нужен.

**Q:** На странице сборок не отображается версия.

**A:** Запускаем "agvtool mvers" и видим что-то в духе: "Cannot find "Restaurants.xcodeproj/../versionNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleShortVersionString" "${PROJECT_DIR}/${INFOPLIST_FILE}")". Необходимо в Build Settings выставить флаг Preprocess Info.plist File в Yes.

**Q:** На странице сборок отображается неверная версия проекта.

**A:** Необходимо в корне проекта запустить команду "agvtool mvers", там будет найдено несколько версий по кол-ву таргетов в проекте. Обычно первой находится версия из основного таргета, но иногда первым оказывается тестовый. Так происходит, например, в случае, если основная папка проекта "Project", а тестов "Project Tests", проблема может быть решена переносом тестов в папку "ProjectTests". В этом случае скрипт вначале дойдет до основного таргета.

**Q:** Exit status of command 'git checkout release/3.0.4' was 128 instead of 0.

**A:** Ошибка обозначает, что fastlane не может переключиться на ветку. Причины: 0) gitlab лежит 1) fastlane в ходе предыдущей сборки внес изменения, которые не получилось откатить - почистите workspace : Jenkins -> iOS.Deploy -> Project.iOS.Deploy -> Workspace -> Wipe Out Current Workspace 2) Ваши lane'ы вносят изменения до смены ветки.

**Q:** 'require': cannot load such file -- some-gem (LoadError)

**A:** Если у вас в проекте есть свой Gemfile, следует добавить в него все зависимости, которые использует наш fastlane-flows.

#### Советы по отладке

- Сейчас все команды fastlane запускаются с флагом `--verbose`. Это лучше не менять - более информативный вывод сильно помогает в отладке.
- Если enterprise-сборка качается, но не запускается, изучите логи телефона в консоли Xcode. Чаще всего там можно узнать подробности ошибок, возникших при установке.
- При проблемах с Code Signing внимательно изучите логи сборки на Jenkins - там можно найти информацию о том, какие профили использовались для подписи.
- Попробуйте повторить все шаги, которые исполняет билд-машина, локально на своем компьютере - если проблема в проекте, так будет проще его отладить.
