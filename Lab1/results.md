## В рамках задачи выполнялось поэлементное умножение двух массивов. Рассмотрены различные подходы - последовательный код и код с применением SSE инструкций

### Результат исполнения последовательного кода c 100000000000 итераций:
**Время выполнения 100000000000 итераций: 5260.2290 мс**

### Результат исполнения кода с SSE с 100000000000 итераций:
**Время выполнения 100000000000 итераций: 1252.6180 мс**

##### Как видно из результатов, выигрыш по времени более чем в 4 раза. Связано это с тем, что во 2 случае напрямую используются SSE инструкции, поддерживаемые процессором и упрощающие работу с массивом в данном случае, так что нет необходимости проводит операции поэлементно.