## В рамках задачи выполнялось сравнение 4 различных коллекций, каждая из которых считала сумму обращений по ключу. Количество ключей задано заранее, а затем в параллельном участке кода происходит обращение по случайному ключу и увеличение счетчика (если обращение по ключу прошло успешно). Затем считается общее количество обращений к Map по всем ключам. 
### Рассмотрены 4 коллекции - потоконебезопасная HashMap, а также потокобезопасные Hashtable, Collections.synchronizedMap и ConcurrentHashMap. Использовалось 30 потоков.

### При работе с HashMap случались ошибки, связанные с конкурентным доступом к определенным ресурсам:
**java.util.HashMapError during access in collection:java.util.HashMap by pool-1-thread-8**\
**Error during access in collection:java.util.HashMap by pool-1-thread-10**\
**Error during access in collection:java.util.HashMap by pool-1-thread-2**\
**Error during access in collection:java.util.HashMap by pool-1-thread-6**\
**Error during access in collection:java.util.HashMap by pool-1-thread-7**

### Было произведено несколько запусков примеров для проверки, и в каждом из них из-за конкурентного доступа терялась часть значений при работе с HaspMap:
**Sample 0: Total sum: 2740485, expected: 3000000**\
**Sample 1: Total sum: 2677400, expected: 3000000**\
**Sample 2: Total sum: 2644840, expected: 3000000**\
**Sample 3: Total sum: 2601034, expected: 3000000**\
**Sample 4: Total sum: 2580613, expected: 3000000**

#### Такие результаты безусловно связаны с тем, что HaspMap является потоконебезопасной коллекцией и не может обеспечить корректный результат при параллельном выполнения, когда нужен конкурентный доступ нескольких потоков к ресурсу.

### Результат исполнения кода с Hashtable:
**Sample 0: Total sum: 3000000, expected: 3000000**\
**Sample 1: Total sum: 3000000, expected: 3000000**\
**Sample 2: Total sum: 3000000, expected: 3000000**\
**Sample 3: Total sum: 3000000, expected: 3000000**\
**Sample 4: Total sum: 3000000, expected: 3000000**

#### Hashtable уже является потокобезопасной коллекцией и может обеспечить корректный результат при конкурентном доступе к бакетам.

### Результат исполнения кода с Collections.synchronizedMap:
**Sample 0: Total sum: 3000000, expected: 3000000**\
**Sample 1: Total sum: 3000000, expected: 3000000**\
**Sample 2: Total sum: 3000000, expected: 3000000**\
**Sample 3: Total sum: 3000000, expected: 3000000**\
**Sample 4: Total sum: 3000000, expected: 3000000**

#### Collections.synchronizedMap также является потокобезопасной коллекцией и может обеспечить корректный результат при конкурентном доступе.

### Результат исполнения кода с ConcurrentHashMap:
**Sample 0: Total sum: 3000000, expected: 3000000**\
**Sample 1: Total sum: 3000000, expected: 3000000**\
**Sample 2: Total sum: 3000000, expected: 3000000**\
**Sample 3: Total sum: 3000000, expected: 3000000**\
**Sample 4: Total sum: 3000000, expected: 3000000**

#### ConcurrentHashMap также является потокобезопасной коллекцией и может обеспечить корректный результат при конкурентном доступе.

### Также было произведено сравнение времени выполнения кода при использовании различных коллекций:

**Execution times:**\
**HashMap: 0,264 s,**\
**HashTable: 1,461 s,**\
**SyncMap: 1,386 s,**\
**ConcurrentHashMap: 0,217 s.**

##### Как видно из результатов, HashMap не стоит использовать, когда необходима коллекция, к которой будет конкурентный доступ. Наиболее быстрой и при этом безопасной коллекцией является ConcurrentHashMap. Связано это с тем, что в отличие от HashTable и synchronizedMap, которые блокируются полностью при доступе к ним, в ConcurrentHashMap блокируются лишь отдельные бакеты, что позволяет другим потокам в это время вести работу с другими бакетами.