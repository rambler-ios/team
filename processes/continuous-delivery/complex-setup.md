### Сложная настройка Continuous Delivery

##### Шаг 1. Jenkins

- Создаем новый проект. При создании выбираем *Copy from existing project: iOS-deploy-config-project*. Название выбираем по формату *Project.Name.iOS.Deploy*.
- В разделе *Source Code Management* вводим адрес git-репозитория проекта.
- Сохраняем изменения.
- Создаем еще один новый проект. При создании выбираем *Copy from existing project: iOS-nightly-config-project*.Название выбираем по формату *Project.Name.iOS.Nightly*.
- В разделе *Source Code Management* вводим адрес git-репозитория проекта.
- Сохраняем изменения.

##### Шаг 2. Настройка Apple Developer Center

- Заведите новый Application Identifier для основного приложения вида `main_app_bundle_id.enterprise`. Проверьте, что все capabilities соответствуют исходному приложению.
- Заведите новые Application Identifiers для всех extension'ов вида `main_app_bundle_id.enterprise.extension_bundle_id`. Проверьте, что все capabilities соответствуют исходным данным.
- Заведите новую Application Group (если использовались в оригинальном приложении) вида `app_group_name.enterprise`. Добавьте ее к тем application identifier'ам, к которым требуется.

##### Шаг 3. Настройка Slack

- Заходите в [настройки нашей команды в Slack](https://***REMOVED***).
- Добавьте новый webhook: *Add Configuration -> Выбираем канал -> Копируем Webhook URL*.

##### Шаг 4. Базовая настройка Fastfile

- В корне вашего проекта создайте папку *fastlane*.
- Заполните файл `.env.default` по [образцу](). Не забудьте добавить полученный на предыдущем шаге webhook.
- Создайте новый `Fastfile` и добавьте в него следующий код:

  ```ruby
  before_all do |lane|
	  import_from_git(url: 'git@***REMOVED***:ramblerco-ios/fastlane-flows.git',
                     path: 'fastlane/Fastfile')
  end
  
  lane :projectname_in_house do |options|
	  in_house(options)
  end
  
  lane :projectname_nightly do |options|
	  nightly(options)
  end
  
  lane :projectname_testing do |options|
	  testing(options)
  end
  
  lane :projectname_staging do |options|
	  staging(options)
  end
  ```
- Заполните `Appfile` по образцу. Не забудьте подставить корректные названия всех lane'ов.

##### Шаг 5. Настройка in-house сборок

- Для того, чтобы скрипт мог поменять названия enterprise-версий всех application identifier'ов, добавьте в Fastfile, в `project_name_in_house` lane, строчку вида:

  ```ruby
options[:extension_identifiers] = ['ru.rambler.news.enterprise','ru.rambler.news.enterprise.watchkit','ru.rambler.news.enterprise.watchkitapp']
```

- Для того, чтобы скрипт мог найти все таргеты, для которых нужно обновить настройки Code Signing, добавьте в Fastfile, в `project_name_in_house` lane, строчку, содержащую паттерны поиска названий таргетов:

  ```ruby
options[:extension_patterns] = ['rnews-ios','rnews-ios WatchKit Extension','rnews-ios WatchKit App']
```

- Для того, чтобы скрипт мог модифицировать содержимое всех *Info.plist* файлов, добавьте в Fastfile, в `project_name_in_house` lane, строчку вида:

  ```ruby
options[:extension_plists] = ['rnews-ios/Supporting Files/Info.plist','rnews-ios WatchKit Extension/Info.plist','rnews-ios WatchKit App/Info.plist']
```

- Добавьте в конец *Fastfile* метод, в котором вручную обновляете различные строчки в plist-файлах, содержащих перекрестные ссылки на разные таргеты, имена Application Groups и прочее. Пример такого метода:

  ```ruby
def update_xcodeproj
      update_info_plist(
        xcodeproj: ENV['XCODEPROJ_NAME'],
        plist_path: 'rnews-ios WatchKit Extension/Info.plist',
        block: lambda { |plist|
          plist['NSExtension']['NSExtensionAttributes']['WKAppBundleIdentifier'] = 'ru.rambler.news.enterprise.watchkitapp'
        }
      )

      update_info_plist(
        xcodeproj: ENV['XCODEPROJ_NAME'],
        plist_path: 'rnews-ios WatchKit App/Info.plist',
        block: lambda { |plist|
          plist['WKCompanionAppBundleIdentifier'] = 'ru.rambler.news.enterprise'
        }
      )

      update_app_group_identifiers(
        entitlements_file: 'rnews-ios/rnews-ios.entitlements',
        app_group_identifiers: ['group.ru.rambler.news.sharedGroup.enterprise']
      )

      update_app_group_identifiers(
        entitlements_file: 'rnews-ios WatchKit Extension/rnews-ios WatchKit Extension.entitlements',
        app_group_identifiers: ['group.ru.rambler.news.sharedGroup.enterprise']
      )
end
```

- Добавьте вызов этого метода в `project_name_in_house` lane:

  ```ruby
lane :news_in_house do |options|
      options[:extension_identifiers] = ['ru.rambler.news.enterprise','ru.rambler.news.enterprise.watchkit','ru.rambler.news.enterprise.watchkitapp']
      options[:extension_patterns] = ['rnews-ios','rnews-ios WatchKit Extension','rnews-ios WatchKit App']
      options[:extension_plists] = ['rnews-ios/Supporting Files/Info.plist','rnews-ios WatchKit Extension/Info.plist','rnews-ios WatchKit App/Info.plist']

      update_xcodeproj

      in_house(options)
end
```

#####  Шаг 6. Настройка nightly сборок

- Обновите `project_name_nightly_lane` по образцу `in_house` lane:

  ```ruby
  lane :news_nightly do |options|
      options[:extension_identifiers] = ['ru.rambler.news.enterprise','ru.rambler.news.enterprise.watchkit','ru.rambler.news.enterprise.watchkitapp']
	  options[:extension_patterns] = ['rnews-ios','rnews-ios WatchKit Extension','rnews-ios WatchKit App']
	  options[:extension_plists] = ['rnews-ios/Supporting Files/Info.plist','rnews-ios WatchKit Extension/Info.plist','rnews-ios WatchKit App/Info.plist']

	  update_xcodeproj

	  nightly(options)
end
  ```
- В настройках проекта `Project.Name.Nightly` на Jenkins поменяйте исполняемый скрипт, подставив туда корректный вызов fastlane:

  ```bash
  #!/bin/bash -l
fastlane news_nightly --verbose
  ```
  
##### Шаг 7. Настройка testing сборок

- Обновите `project_name_testing_lane` по образцу `in_house` lane, но используя не enterprise identifier'ы:

  ```ruby
  lane :news_testing do |options|
      options[:extension_identifiers] = ['ru.rambler.news','ru.rambler.news.watchkit','ru.rambler.news.watchkitapp']
	  options[:extension_patterns] = ['rnews-ios','rnews-ios WatchKit Extension','rnews-ios WatchKit App']
	  options[:extension_plists] = ['rnews-ios/Supporting Files/Info.plist','rnews-ios WatchKit Extension/Info.plist','rnews-ios WatchKit App/Info.plist']

	  testing(options)
end
  ```
  
- В файл `.env.default` добавьте список групп Fabric, которым нужно автоматически рассылать билд. Группа RDS QA включена по умолчанию.

  ```
  FABRIC_GROUPS=group1,group2,group3
  ```
  
##### Шаг 8. Настройка staging сборок

- Обновите `project_name_staging_lane` по образцу `testing` lane:

  ```ruby
  lane :news_testing do |options|
      options[:extension_identifiers] = ['ru.rambler.news','ru.rambler.news.watchkit','ru.rambler.news.watchkitapp']
	  options[:extension_patterns] = ['rnews-ios','rnews-ios WatchKit Extension','rnews-ios WatchKit App']
	  options[:extension_plists] = ['rnews-ios/Supporting Files/Info.plist','rnews-ios WatchKit Extension/Info.plist','rnews-ios WatchKit App/Info.plist']

	  staging(options)
end
  ```