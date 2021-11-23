# Типы кортежей (справочник по C#)

-   28.09.2021
-   Чтение занимает 3 мин
-   -   [![](https://github.com/BillWagner.png?size=32)](https://github.com/BillWagner "BillWagner")
    -   [![](https://github.com/olprod.png?size=32)](https://github.com/olprod "olprod")

Были ли сведения на этой странице полезными?

_Кортежи_, доступные в C# 7.0 и более поздних версиях, предоставляют краткий синтаксис для группирования нескольких элементов данных в упрощенную структуру данных. В следующем примере показано, как можно объявить переменную кортежа, инициализировать ее и получить доступ к ее элементам данных.

C#Копировать

Выполнить

```
(double, int) t1 = (4.5, 3);
Console.WriteLine($"Tuple with elements {t1.Item1} and {t1.Item2}.");
// Output:
// Tuple with elements 4.5 and 3.

(double Sum, int Count) t2 = (4.5, 3);
Console.WriteLine($"Sum of {t2.Count} elements is {t2.Sum}.");
// Output:
// Sum of 3 elements is 4.5.
```

Как показано в предыдущем примере, для определения типа кортежа необходимо указать типы всех его элементов данных и, при необходимости, [имена полей](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-field-names). В типе кортежа невозможно определить методы, но можно использовать методы, предоставляемые .NET, как показано в следующем примере.

C#Копировать

Выполнить

```
(double, int) t = (4.5, 3);
Console.WriteLine(t.ToString());
Console.WriteLine($"Hash code of {t} is {t.GetHashCode()}.");
// Output:
// (4.5, 3)
// Hash code of (4.5, 3) is 718460086.
```

Начиная с C# 7.3, типы кортежей поддерживают [операторы равенства](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/equality-operators) `==` и `!=`. Дополнительные сведения см. в разделе [Равенство кортежей](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-equality).

Типы кортежей являются [типами значений](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-types), а элементы кортежа — общедоступными полями. Поэтому кортежи представляют собой _изменяемые_ типы значений.

 Примечание

Для кортежей требуется тип [System.ValueTuple](https://docs.microsoft.com/ru-ru/dotnet/api/system.valuetuple) и связанные универсальные типы (например, [System.ValueTuple<T1,T2>](https://docs.microsoft.com/ru-ru/dotnet/api/system.valuetuple-2)), доступные в .NET Core и .NET Framework 4.7 и более поздних версий. Чтобы использовать кортежи в проекте, предназначенном для .NET Framework 4.6.2 или более ранней версии, добавьте в проект пакет NuGet [`System.ValueTuple`](https://www.nuget.org/packages/System.ValueTuple/).

Можно определить кортежи со сколь угодно большим числом элементов.

C#Копировать

Выполнить

```
var t = 
(1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
11, 12, 13, 14, 15, 16, 17, 18,
19, 20, 21, 22, 23, 24, 25, 26);
Console.WriteLine(t.Item26);  // output: 26
```

## [](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#use-cases-of-tuples)Варианты использования кортежей

Чаще всего кортежи используются как возвращаемый методом тип. То есть вместо определения [параметров метода `out`](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/out-parameter-modifier) можно сгруппировать результаты метода в возвращаемый тип кортежа, как показано в следующем примере.

C#Копировать

Выполнить

```
var xs = new[] { 4, 7, 9 };
var limits = FindMinMax(xs);
Console.WriteLine($"Limits of [{string.Join(" ", xs)}] are {limits.min} and {limits.max}");
// Output:
// Limits of [4 7 9] are 4 and 9

var ys = new[] { -9, 0, 67, 100 };
var (minimum, maximum) = FindMinMax(ys);
Console.WriteLine($"Limits of [{string.Join(" ", ys)}] are {minimum} and {maximum}");
// Output:
// Limits of [-9 0 67 100] are -9 and 100

(int min, int max) FindMinMax(int[] input)
{
    if (input is null || input.Length == 0)
    {
        throw new ArgumentException("Cannot find minimum and maximum of a null or empty array.");
    }

    var min = int.MaxValue;
    var max = int.MinValue;
    foreach (var i in input)
    {
        if (i < min)
        {
            min = i;
        }
        if (i > max)
        {
            max = i;
        }
    }
    return (min, max);
}
```

Как показано в предыдущем примере, с возвращаемым экземпляром кортежа можно работать напрямую или [деконструировать](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-assignment-and-deconstruction) его в отдельные переменные.

Типы кортежей можно также использовать вместо [анонимных типов](https://docs.microsoft.com/ru-ru/dotnet/csharp/fundamentals/types/anonymous-types), например в запросах LINQ. Дополнительные сведения см. в статье [Выбор между анонимными типами и кортежами](https://docs.microsoft.com/ru-ru/dotnet/standard/base-types/choosing-between-anonymous-and-tuple).

Как правило, кортежи используются для группирования слабо связанных элементов данных. Это целесообразно в закрытых и внутренних служебных методах. При работе с общедоступным API рассмотрите возможность определения типа [класса](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/class) или [структуры](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/struct).

## [](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-field-names)Имена полей кортежей

Имена полей кортежей указываются явным образом либо в выражении инициализации кортежа, либо в определении типа кортежа, как показано в следующем примере.

C#Копировать

Выполнить

```
var t = (Sum: 4.5, Count: 3);
Console.WriteLine($"Sum of {t.Count} elements is {t.Sum}.");

(double Sum, int Count) d = (4.5, 3);
Console.WriteLine($"Sum of {d.Count} elements is {d.Sum}.");
```

Начиная с C# 7.1, если имя поля не указано, оно может быть выведено из имени соответствующей переменной в выражении инициализации кортежа, как показано в следующем примере.

C#Копировать

Выполнить

```
var sum = 4.5;
var count = 3;
var t = (sum, count);
Console.WriteLine($"Sum of {t.count} elements is {t.sum}.");
```

Это называется инициализаторами проекций кортежа. Имя переменной не проецируется на имя поля кортежа в следующих случаях:

-   Имя кандидата — это имя элемента типа кортежа, например `Item3`, `ToString`или `Rest`.
-   Имя кандидата является дубликатом другого имени поля кортежа, явного или неявного.

В этих случаях необходимо либо явно указать имя поля, либо получить доступ к полю по имени по умолчанию.

По умолчанию поля кортежа имеют имена `Item1`, `Item2`, `Item3` и т. д. Всегда можно использовать имя поля по умолчанию, даже если имя поля указано явно или является выводимым, как показано в следующем примере.

C#Копировать

Выполнить

```
var a = 1;
var t = (a, b: 2, 3);
Console.WriteLine($"The 1st element is {t.Item1} (same as {t.a}).");
Console.WriteLine($"The 2nd element is {t.Item2} (same as {t.b}).");
Console.WriteLine($"The 3rd element is {t.Item3}.");
// Output:
// The 1st element is 1 (same as 1).
// The 2nd element is 2 (same as 2).
// The 3rd element is 3.
```

Имена полей не учитываются при [присваивании кортежа](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-assignment-and-deconstruction) и [сравнении кортежей на равенство](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-equality).

Во время компиляции компилятор заменяет имена полей не по умолчанию соответствующими именами по умолчанию. В результате явно указанные или выводимые имена полей будут недоступны во время выполнения.

## [](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-assignment-and-deconstruction)Присваивание и деконструкция кортежей

В C# поддерживается присваивание между типами кортежей, которые соответствуют обоим следующим условиям:

-   оба типа кортежей должны содержать одинаковое количество элементов;
-   для каждой позиции кортежа тип правого элемента кортежа аналогичен типу соответствующего левого элемента кортежа или может быть неявно преобразован в этот тип.

Значения элементов кортежа присваиваются в порядке расположения элементов кортежа. Имена полей кортежа не учитываются и не присваиваются, как показано в следующем примере.

C#Копировать

Выполнить

```
(int, double) t1 = (17, 3.14);
(double First, double Second) t2 = (0.0, 1.0);
t2 = t1;
Console.WriteLine($"{nameof(t2)}: {t2.First} and {t2.Second}");
// Output:
// t2: 17 and 3.14

(double A, double B) t3 = (2.0, 3.0);
t3 = t2;
Console.WriteLine($"{nameof(t3)}: {t3.A} and {t3.B}");
// Output:
// t3: 17 and 3.14
```

Оператор присваивания `=` можно также использовать для _деконструкции_ экземпляра кортежа в отдельные переменные. Существует три способа деконструкции кортежа.

-   Вы можете явно объявить тип каждой переменной в скобках.
    
    C#Копировать
    
    Выполнить
    
    ```
    var t = ("post office", 3.6);
    (string destination, double distance) = t;
    Console.WriteLine($"Distance to {destination} is {distance} kilometers.");
    // Output:
    // Distance to post office is 3.6 kilometers.
    ```
    
-   Вы можете использовать ключевое слово `var` за пределами круглых скобок, чтобы объявить неявно типизированные переменные и позволить компилятору вывести их типы.
    
    C#Копировать
    
    Выполнить
    
    ```
    var t = ("post office", 3.6);
    var (destination, distance) = t;
    Console.WriteLine($"Distance to {destination} is {distance} kilometers.");
    // Output:
    // Distance to post office is 3.6 kilometers.
    ```
    
-   Вы можете использовать существующие переменные.
    
    C#Копировать
    
    Выполнить
    
    ```
    var destination = string.Empty;
    var distance = 0.0;
    
    var t = ("post office", 3.6);
    (destination, distance) = t;
    Console.WriteLine($"Distance to {destination} is {distance} kilometers.");
    // Output:
    // Distance to post office is 3.6 kilometers.
    ```
    

Подробнее о деконструкции кортежей с помощью и других типов см. в статье [Деконструкция кортежей и других типов](https://docs.microsoft.com/ru-ru/dotnet/csharp/fundamentals/functional/deconstruct).

## [](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuple-equality)Равенство кортежей

Начиная с C# 7.3, типы кортежей поддерживают операторы `==` и `!=`. Эти операторы сравнивают элементы левого операнда с соответствующими элементами правого операнда в соответствии с порядком расположения элементов кортежа.

C#Копировать

Выполнить

```
(int a, byte b) left = (5, 10);
(long a, int b) right = (5, 10);
Console.WriteLine(left == right);  // output: True
Console.WriteLine(left != right);  // output: False

var t1 = (A: 5, B: 10);
var t2 = (B: 5, A: 10);
Console.WriteLine(t1 == t2);  // output: True
Console.WriteLine(t1 != t2);  // output: False
```

Как показано в предыдущем примере, в операциях `==` и `!=` не учитываются имена полей кортежей.

Два кортежа сравнимы, если выполнены оба следующих условия:

-   оба кортежа содержат одинаковое количество элементов. Например, `t1 != t2` не компилируется, если `t1` и `t2` имеют разное количество элементов.
-   Для каждой позиции кортежа соответствующие элементы из левого и правого операндов кортежа сравниваются с помощью операторов `==` и `!=`. Например, `(1, (2, 3)) == ((1, 2), 3)` не компилируется, поскольку `1` не сравнивается с помощью `(1, 2)`.

Операторы `==` и `!=` сравнивают кортежи с сокращенной обработкой. Это значит, что операция останавливается, как только она соответствует паре неравных элементов или достигает конца кортежей. Однако перед любым сравнением _все_ элементы кортежа вычисляются, как показано в следующем примере.

C#Копировать

Выполнить

```
Console.WriteLine((Display(1), Display(2)) == (Display(3), Display(4)));

int Display(int s)
{
    Console.WriteLine(s);
    return s;
}
// Output:
// 1
// 2
// 3
// 4
// False
```

## [](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuples-as-out-parameters)Кортежи как параметры вывода

Как правило, вы выполняете рефакторинг метода, имеющего [параметры `out`](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/out-parameter-modifier), в метод, возвращающий кортеж. Однако бывают случаи, когда параметр `out` может иметь тип кортежа. В следующем примере показано, как работать с кортежами в виде параметров `out`.

C#Копировать

Выполнить

```
var limitsLookup = new Dictionary<int, (int Min, int Max)>()
{
    [2] = (4, 10),
    [4] = (10, 20),
    [6] = (0, 23)
};

if (limitsLookup.TryGetValue(4, out (int Min, int Max) limits))
{
    Console.WriteLine($"Found limits: min is {limits.Min}, max is {limits.Max}");
}
// Output:
// Found limits: min is 10, max is 20
```

## [](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#tuples-vs-systemtuple)Кортежи и `System.Tuple`

Кортежи C# с типами [System.ValueTuple](https://docs.microsoft.com/ru-ru/dotnet/api/system.valuetuple), отличаются от кортежей, представленных типами [System.Tuple](https://docs.microsoft.com/ru-ru/dotnet/api/system.tuple). Основные различия заключаются в следующем.

-   Типы `ValueTuple` являются [типами значений](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-types). Типы `Tuple` являются [ссылочными типами](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/reference-types).
-   Типы `ValueTuple` являются изменяемыми. Типы `Tuple` являются неизменяемыми.
-   Элементами данных типов `ValueTuple` являются поля. Элементами данных типов `Tuple` являются свойства.

## [](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-tuples#c-language-specification)Спецификация языка C#

Дополнительные сведения см. в следующих примечаниях к предлагаемой функции.

-   [Выводимые имена кортежей (инициализаторы проекций кортежа)](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/proposals/csharp-7.1/infer-tuple-names)
-   [Поддержка `==` и `!=` для типов кортежей](https://docs.microsoft.com/ru-ru/dotnet/csharp/language-reference/proposals/csharp-7.3/tuple-equality)