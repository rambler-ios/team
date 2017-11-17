### Архитектурные подходы

В качестве основной архитектуры проектов используется [multitier architecture](https://en.wikipedia.org/wiki/Multitier_architecture), в общем случае состоящая из двух слоев - Presentation, содержащего конкретные user story, и Business Logic, содержащего независимую от конкретных use case'ов логику.

На Presentation слое используется VIPER. Очень подробно о нем мы рассказали в нашей [The Book of VIPER](https://github.com/rambler-ios/The-Book-of-VIPER). 

На слое бизнес-логики мы используем [Service Oriented Architecture](https://en.wikipedia.org/wiki/Service-oriented_architecture). Подробнее об этом мы рассказывали [на одном из наших митапов](https://www.youtube.com/watch?v=9BpKSxcST-Q).

Принципы, применяемые при разработке: [SOLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)), [TDD](https://en.wikipedia.org/wiki/Test-driven_development).