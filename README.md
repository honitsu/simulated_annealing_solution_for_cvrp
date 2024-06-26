Данный код решает [транспортную задачу](https://ru.wikipedia.org/wiki/%D0%A2%D1%80%D0%B0%D0%BD%D1%81%D0%BF%D0%BE%D1%80%D1%82%D0%BD%D0%B0%D1%8F_%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D0%B0) методом [имитации отжига](https://ru.wikipedia.org/wiki/%D0%90%D0%BB%D0%B3%D0%BE%D1%80%D0%B8%D1%82%D0%BC_%D0%B8%D0%BC%D0%B8%D1%82%D0%B0%D1%86%D0%B8%D0%B8_%D0%BE%D1%82%D0%B6%D0%B8%D0%B3%D0%B0).

Программа читает очередной .vrp-файл из папки datafiles, 
делает начальное распределение клиентов по маршрутам 2-мя способами:
сначала клиенты расставляются по маршрутам в случаййном порядке, а в случае
неудачи список сортируется по demands по убыванию и клиенты расставляются также
в случайном порядке, но отсортированный список позволяет выполнить расстановку для 
задач с высоким коэффициентом ratio.

Выполняется 2 вида перестановок клиентов:
 - 1 клиент переносится из одного маршрута в другой;
 - 2 клиента меняются местами в одном и том же или разных маршрутах.

После этого проверяется корректность значения capacity и суммы demands на маршрутах
и проверяется суммарная длина маршрута.
После успешной проверки выполняется оптимизация положения клента -
перебираются все позиции данного клиента на маршруте и выбирается лучшая.
При улучшении маршрутов - происходит переход.
При ухудшении переход совершается с вероятностью exp(-|x0-x|/T).
