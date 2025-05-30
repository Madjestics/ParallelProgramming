## В рамках задачи выполнялось вычисление корня различных чисел. Рассмотрен подход с применением OpenMP. Произведено сравнение результатов с последовательной программой и программой с Pthreads из предыдущей лабораторной работы

### Результат исполнения последовательного кода c 10 потоками (из 2 лабораторной):
**Время выполнения на 10 потоках (последовательно): 5565.0850 мс**

### Результат исполнения кода с pthreads с 10 потоками (из 2 лабораторной):
**Время выполнения на 10 потоках (pthreads): 589.4090 мс**

### Результат исполнения кода с OpenMP с 10 потоками:
**Время выполнения на 10 потоках (openmp): 528.9340 мс**
### При этом также выводится количество OpenMP потоков: 
**OpenMP threads: 10**

#### Из результатов видно, что наибольшее преимущество по времени дает именно OpenMP, так как является по сути совокупностью директив для компилятора вместо ручного создания потоков, как в случае pthreads. Таким образом, компилятор может применять различные оптимизации кода. Также OpenMP уменьшает накладные расходы за счет использования пула потоков, создающегося единожды, вместо ручного управления потоками как в pthreads.****
