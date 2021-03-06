# **Отчёт о тестировании приложения Money Transfer**
# Краткое описание
10.03.2021 было создано и протестировано приложение с рабочим названием Money Transfer. В качестве исходных данных заказчик предложил следующие:

- текущий баланс счёта клиента - переменная типа *int*, значение - 2_000_000_000 (два миллиарда рублей)*
- сумма перевода - переменная типа *int*, значение - 500_000_000 (пятьсот миллионов рублей)
- переменная для хранения итогового значения - тип *int*

**Задача:** протестировать поведение приложения с данными заказчика, проанализировать возможные проблемы, дать рекомендации о проделанной работе.

В качестве переменных были использованы
- **balance** = текущий баланс
- **transfer** = сумма перевода
- **total** = итоговое значение

# Описание тестов
Всего было проведено 6 тестов - smoke-тест приложения, и далее 5 функциональных тестов методом белого ящика с использованием эквивалентных значений:
1. **(passed)** smoke-тест - в качестве входных данных использованы balance=2, transfer=2. Приложение вернуло в качестве результата total=4, что верно (2+2=4);
2. **(failed)** всем переменным назначен тип int. Ожидаемый результат 2 500 000 000, фактический -1 794 967 296;
3. **(failed)** переменным balance и transfer назначен тип int, а переменной total - тип long. Ожидаемый результат 2 500 000 000, фактический -1 794 967 296;
4. **(failed)** переменным balance и transfer назначен тип long, переменной total - тип int. Ожидаемый результат 2 500 000 000, фактический - приложение не запускается с информацией компилятора **«java: incompatible types: possible lossy conversion from long to int»**
5. **(passed)** переменной balance назначен тип int, а переменным transfer и total - тип long. Ожидаемый результат 2 500 000 000, фактический 2 500 000 000;
6. **(passed)** всем переменным назначен тип long. Ожидаемый результат 2 500 000 000, фактический 2 500 000 000;

# Результаты
- Из 6-ти тестов 3 успешных = (50)
- [Баг-репорт](https://github.com/albertooo00/Money.Transfer/issues/1)
# Общие рекомендации
В процессе тестирования, обноружено несоответсвие выбранного заказчиком типа данных т.к. реальные суммы  переводов могут превысить границы типа int.
В данной ситуации следует использовать тип long, позволяющий хранить значения до 9 223 372 036 854 775 807