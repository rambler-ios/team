# Как делать сборки

1. У вас должны быть выставлены права на создание сборок на Jenkins.

  ![Screenshot](/resources/deploy-guide-1.jpg)

2. Зайдите на вкладку iOS.Deploy на Jenkins. Выберите нужный проект.

  ![Screenshot](/resources/deploy-guide-2.jpg)

3. В боковом меню выберите пункт *Build with parameters*.

  ![Screenshot](/resources/deploy-guide-3.jpg)

4. Выберите требуемый тип сборки. Подробнее о них можно почитать на [другой странице](/processes/continuous-delivery/workflows.md).

  ![Screenshot](/resources/deploy-guide-4.jpg)

5. Для staging-сборок укажите номер версии.
6. Нажмите кнопку Build. На главной странице Jenkins эта задача появится в общей очереди. Прогресс сборки показывается индикатором.

  ![Screenshot](/resources/deploy-guide-5.jpg)
