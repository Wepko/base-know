# Тип данных tuple, кортеж (DOCS Python3)
1.  [Справочник по языку Python3.](https://docs-python.ru/tutorial/ "Руководство по программированию на Python3.")
2.  [Основные встроенные типы Python](https://docs-python.ru/tutorial/osnovnye-vstroennye-tipy-python/ "Основные типы языка Python")
3.  Тип данных tuple, кортеж

Кортежи - это **_неизменяемые последовательности_**, обычно используемые для хранения коллекций разнородных данных. Например двойной кортеж, создаваемый [встроенной функцией enumerate()](https://docs-python.ru/tutorial/vstroennye-funktsii-interpretatora-python/funktsija-enumerate/ "Функция enumerate() в Python, счетчик элементов последовательности."). Кортежи также используются в тех случаях, когда требуется неизменяемая последовательность однородных данных.


Для кортежей доступны все [общие операции с последовательностями](https://docs-python.ru/tutorial/obschie-operatsii-posledovatelnostjami-list-tuple-str-python/ "Общие операции с последовательностями list, tuple, str в Python").

В Python кортежи представлены [классом `tuple()`](https://docs-python.ru/tutorial/osnovnye-vstroennye-tipy-python/tip-dannyh-tuple-kortezh/ "Тип данных tuple, кортеж").

Кортежи могут быть созданы несколькими способами:

1.  Используя пару скобок для обозначения пустого кортежа: `()`.
2.  Использование запятой для одиночного кортежа: `a,` или `(a,)`.
3.  Разделение элементов запятыми: `a, b, c` или `(a, b, c)`:  
    Обратите внимание, что запятая создает кортеж, а не скобки. Скобки необязательны, за исключением случая пустого кортежа, или когда они необходимы, чтобы избежать синтаксической двусмысленности.  
    Например:
    -   `f(a, b, c)` - вызов функции с тремя аргументами,
    -   `f((a, b, c))` - вызов функции с кортежем в качестве единственного аргумента.
4.  Использование встроенного класса `tuple()`:
    -   `tuple()` - создаст пустой кортеж,
    -   `tuple(iterable)` - преобразует контейнер, поддерживающим итерацию в кортеж.

Конструктор класса `tuple()` создает кортеж, элементы которого **_совпадают и находятся в том же порядке_**, что и элементы итератора `iterable`. Аргумент `iterable` может быть либо [последовательностью](https://docs-python.ru/tutorial/osnovnye-vstroennye-tipy-python/tipy-posledovatelnostej/ "Типы последовательностей"), [контейнером поддерживающим итерацию](https://docs-python.ru/tutorial/osnovnye-vstroennye-tipy-python/tip-dannyh-generator-generator/ "Тип данных generator (генератор)."), либо [объектом итератора](https://docs-python.ru/tutorial/osnovnye-vstroennye-tipy-python/tip-dannyh-iterator-iterator/ "Тип данных Iterator (итератор)."). Если `iterable` уже является кортежем, он возвращается без изменений. Если аргумент не задан, конструктор создает новый пустой кортеж `()`.

Для разнородных коллекций данных, где доступ по имени более понятен, чем [доступ по индексу](https://docs-python.ru/tutorial/obschie-operatsii-posledovatelnostjami-list-tuple-str-python/izvlechenie-elementa-sequence-indeksu/ "Получение значения элемента по индексу sequence[i] в Python."), [`collections.namedtuple()`](https://docs-python.ru/standart-library/modul-collections-python/klass-namedtuple-modulja-collections/ "Класс namedtuple() модуля collections в Python.") может быть более подходящим выбором, чем простой [объект кортежа](https://docs-python.ru/tutorial/osnovnye-vstroennye-tipy-python/tip-dannyh-tuple-kortezh/ "Тип данных tuple, кортеж").

#### Примеры использования создания кортежа и преобразования объектов к типу `tuple`:
```
# Создание кортежа тип tuple
>>> ()
# ()
>>> tuple()
# ()
>>> 105,
# (105,)
>>> 1, 'a', 3, 'b'
# (1, 'a', 3, 'b')

# Преобразование строки str в кортеж тип tuple
>>> tuple('abc')
# ('a',' b',' c')

# Преобразование списка list в кортеж тип tuple
>>> tuple([1, 2, 3])
# (1, 2, 3)

# Преобразование множества set в кортеж тип tuple
>>> tuple({1, 2, 3})
# (1, 2, 3)

# Преобразование генератора в кортеж тип tuple
>>> tuple(range(5))
# (0, 1, 2, 3, 4)
```