# Начало нового проекта

### Выбор bundle id

Для bundle id используется идентификатор вида `ru.ramblerco.[название компании].[название проекта]`.

**Примеры:** `ru.ramblerco.rambler.mail`, `ru.ramblerco.rambler.news`, `ru.ramblerco.afisha.restaurants`.

### GitLab

В namespace `ramblerco-ios` на корпоративном GitLab создайте новый проект. Название репозитория должно совпадать с bundle id.

### Continuous Integration

В качестве инструмента Continuous Integration для неактивных проектов используется Jenkins. [Инструкцию](/processes/automation/continuous-integration/jenkins-ci-setup.md) по его настройке следует использовать при возобновлении активной поддержки проекта или исправлению ошибок.

Для всех новых и активных проектов в качестве инструмента Continuous Integration используется GitLab CI. Инструкция по его настройке находится в данный момент [в разработке](https://github.com/rambler-ios/team/issues/116). 

### Continuous Delivery

В качестве инструмента Continuous Delivery для неактивных проектов используется Jenkins. [Инструкцию](/processes/automation/continuous-delivery/README.md#Настройка) по его настройке следует использовать при возобновлении активной поддержки проекта или исправлению ошибок.

Для всех новых и активных проектов в качестве инструмента Continuous Delivery используется GitLab CI. Инструкция по его настройке находится в данный момент [в разработке](https://github.com/rambler-ios/team/issues/117). 

Также в качестве инструмента для автоматизации процесса CD используется [Ramb-n-roll](https://github.com/rambler-digital-solutions/rambnroll), выкладка которого в open-source планируется после завершения разработки первой версии инструмента. 

### Upsource

Попросите вашего руководителя настроить новый проект на Upsource.