# Continuous Delivery

В общем виде Continuous Delivery - это набор методик, которые позволяют обеспечить возможность доставки приложения в любой момент времени. В нашем случае - это автоматизация заливки билда приложения в различные сервисы: Artifactory, Fabric, TestFlight.

Управление процессом осуществляется через 

- корпоративный Jenkins для неактивных проектов. Подробная инструкция по запуску билдов - [тут](/processes/automation/continuous-delivery/guide.md).
- через GitLab CI для новых и активных проектов. Инструкция [в работе](https://github.com/rambler-ios/team/issues/117).

Отдельное внимание стоит обратить на тот факт, что мы автоматизируем не механизмы заливки архива в разные источники, а именно workflow работы со сборками. Об этих процессах знают команда и бизнес, благодаря им нивелируются требования вроде *"Соберите мне сборку в Fabric, в которой будут те две фичи, сегодняшний коммит и обязательно вот эта новая иконка"*. Подробнее о видах сборок, используемых в компании, можно прочитать [здесь](/processes/automation/continuous-delivery/workflows.md).

### Настройка Jenkins

Есть два варианта настройки проекта:

- [Упрощенный](/processes/automation/continuous-delivery/simple-setup.md)

  У приложения нет дополнительных extension'ов
  
- [Сложный](/processes/automation/continuous-delivery/complex-setup.md)

  Нужен для приложений с extension'ами (Apple Watch и т.п.)

В отдельных случаях могут быть добавлены свои workflow, используя готовые приватные lane, закрывающие непосредственно механизмы доставки (Artifactory, Fabric, TestFlight).

Если при настройке или использовании CD возникли какие-то проблемы, поищите решения в [разделе Troubleshooting](/processes/automation/continuous-delivery/troubleshooting.md).

