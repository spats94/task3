# Тестовое задание 3

Объект управления описывается уравнением состояния с нелинейным коэффициентом

![Безымянный](https://quicklatex.com/cache3/c8/ql_9de290c9549a3c69bd0f19b270c415c8_l3.png)

где 

![Безымянный](https://quicklatex.com/cache3/a4/ql_303b529ed164d325737875258398daa4_l3.png)

Необходимо спроектировать структуру регулятора для объекта управления,
вычисляющий управляющие воздействие u для объекта управления такое, что в
установившемся процессе значение выходного сигнала y равно значению уставки yref c
нулевой ошибкой. Регулятор должен работать с периодом дискретизации 10 мсек.
Структура регулятора должна позволять путём калибровки на объекте достичь постоянства
времени переходного процесса системы регулятор – объект управления при условии
постоянства сигнала V для любого из двух значений коэффициента A.

### Модель объекта и регулятора в симулинке

Для регулирования, был выбрал PID(z) регулятор,  он достаточно просто, чтобы работать с дискретизацией 10мс, а также есть возможность преобразовать в с код. Настройки регулятора представлены ниже.

![Безымянный](https://i.ibb.co/5GTQ0n1/image.jpg)

### Объект управления

Объект управления создан с помощью базисных блоков simulink

![Безымянный1](https://i.ibb.co/BTcfhbc/1.png)

А также, коэффициент A задается с помощью блока Relay

![Безымянный2](https://i.ibb.co/LQknLZt/2.png)

В целом система выглядит следующим образом.

![Безымянный3](https://i.ibb.co/pPzDJbm/3.png)

### Калибровка регулятора

Для калибровки, используется утилита PID Tune

Этапы калибровки регулятора:

1) Идентификация системы

Для идентификации системы, создаем набор данных вход-выход, для этого используется модель ident.slx/, которая проводит моделирование системы и записывает в переменную y реакцию на единичный скачек

Далее в PID Tuner идентифицируем новый plant.

2) Подбор коэффициентов: подбираем такие коэффициенты, которые будут удовлетворять нашим параметрам. Возьмем что нам необходимо для обоих коэффициентов А время переходного процесса 3 сек.

Для А1 были получены коэффициенты

kP1=4.6957
kI1=23.4784
kD1=0

Аналогично проводим для А2

kP2=7.0492
kI2=28.158
kD2=0.30826

### Результат

В результате имеем одинаковое время переходного процесса

![1569421215089](https://i.ibb.co/DgGm3gg/4.png)



