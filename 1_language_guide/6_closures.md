## Замикання

*Замикання* – це самодостатні блоки функціональності, що можуть передаватись та використовуватись у коді. Замикання у Swift є аналогічними блокам в C та Objective-C, і лямбдам в інших мовах програмування.

Замикання можуть захоплювати і зберігати посилання на константи та змінні з контексту, в якому вони оголошені. Цю поведінку називають *замиканням на* константи та змінні. Swift бере на себе все управління пам'яттю при захопленні змінних.

> **Note**
> 
> Не слід переживати, якщо ви не знайомі з концепцією захоплення. Вона детально описана нижче у підрозділі [Захоплення значень](#Захоплення-значень).

Глобальні та вкладені функції, які представлені в попередньому розділі [Функції](5_functions.md), є особливими випадками замикань. Загалом, замикання можуть приймати одну із трьох форм:

 + Глобальні функції є замиканнями, що мають ім'я та не захоплюють значень.
 + Вкладені функції є замиканнями, що мають ім'я та захоплюють значення із функції, де їх оголошено.
 + Вирази замикань є безіменними замиканнями, що записуються за допомогою легковісного синтаксису та можуть захоплювати значення із довколишнього контексту.

У Swift вирази замикань мають чистий, зрозумілий стиль, з оптимізаціями, котрі заохочують которкий, незахаращений синтаксис у найчастіших сценаріях. Ці оптимізації включають:

 + Виведення типів параметрів та значення, що повертається, з контексту
 + Неявний `return` у замиканнях, що складаються з одного рядка
 + Скорочений запис імен аргументів
 + Синтаксис прикінцевих замикань

### Вирази замикань

Вкладені функції, як показано у підрозділі [Вкладені функції](5_functions.md#Вкладені-функції), є зручним засобом визначення та іменування самодостатніх блоків коду в якості частини більшої функції. Однак, іноді корисно писати коротші версії функцієподібних конструктів без повного оголошення та імені. Це найбільш доречно при роботі із функціями чи методами, що приймають інші функції в якості одного чи кілької аргументів.

Вирази замикань є способом запису замикання по місцю використання за допомогою короткого, зосередженого синтаксису. Синтаксис виразів замикань має кілька оптимізацій, потрібних для запису замикань у найкоротшій формі без втрати ясності чи наміру. Приклади виразів замикань нижче ілюструють ці оптимізації шляхом удосконалення одного прикладу із методом `sorted(by:)` протягом кількох ітерацій, у кожній з яких одна й та ж функціональність буде записана у більш лаконічний спосіб.

#### Метод Sorted

Стандартна бібліотека Swift надає метод на ім'я `sorted(by:)`, котрий сортує масив значень відомого типу, в залежності від результату сортуючого замикання, що ви надаєте. Після завершення процесу сортування, метод `sorted(by:)` повертає новий масив також ж типу і розміру, як і старий, із елементами, котрі відсортовані у відповідному порядку. Початковий масив методом `sorted(by:)` не змінюється.

У прикладі нижче використовується метод `sorted(by:)` для сортування масиву значень `String` у зворотньому алфавітному порядку. Ось початковий масив для сортування:

The closure expression examples below use the `sorted(by:)` method to sort an array of `String` values in reverse alphabetical order. Here’s the initial array to be sorted:

```swiftlet names = ["В'ячеслав", "Сергій", "Анна", "Ярослав", "Святослав"]
```

Метод `sorted(by:)` приймає замикання, що бере два аргументи того ж типу, що й вміст масиву, та повертає булеве значення, котре вказує, чи є повинно йти перше значення перед другим після сортування масиву. Замикання, що сортує, повинно поветрати `true`, якщо перше значення повинно йти *перед* другим значенням, і `false` в інакшому випадку.

У цьому прикладі відсортовуєтсья масив значень типу `String`, і тому типом замикання, що сортує, має бути функція типу `(String, String) -> Bool`.

Одним із способів надати замикання, що сортує, є написання звичайної функції коректного типу, і передача її як аргумент в метод `sorted(by:)`:

```swiftfunc backward(_ s1: String, _ s2: String) -> Bool {    return s1 > s2}var reversedNames = names.sorted(by: backward)// reversedNames дорівнює ["Ярослав", "Сергій", "Святослав", "В'ячеслав", "Анна"]
```

Якщо перший рядок (`s1`) більший за другий рядок (`s2`), функція `backward(_:_:)` поверне `true`, вказуючи, що у відсортованому масиві рядок `s1` повинен іти перед рядком `s2`. Для символів у рядку, “більше ніж” означає “з'являється у алфафілі після”. Це означає, що літера `"Б"` є “більшою ніж” літера `"А"`, а рядок `"віл"` є більшим за рядок `"вал"`. Це й призводить до зворотнього алфавітного сортування, де `"Богдан"` знаходиться перед `"Анна"`, і так далі.

Однак, це досить довготривалий шлях для запису того, що є по суті функцією з одного виразу (`a > b`). В цьому прикладі було би доречніше записати замикання, що сортує, одразу в місці використання, використовуючи синтаксис виразів замикань.
#### Синтаксис виразів замикань

Синтаксис виразів замикань має наступний загальний вигляд:

```swift{ (<параметри>) -> <тип, що повертається> in    <інструкції>}
```

*Параметри* у виразах замикань можуть бути двонаправленими, але не можуть мати значень за замовчанням. Варіативні параметри також можуть використовуватись у виразах замикань. Кортежі можуть використовуватись і як параметри, і як значення, що повертається.

У наступному прикладі продемонстровано вираз замикання замість функції `backward(_:_:)` з попереднього прикладу:

```swiftreversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in    return s1 > s2})
```

Слід помітити, що оголошення параметрів та типу, що повертається, для цього замикання є ідентичним до такого ж оголошення в функції `backward(_:_:)`. В обох випадках, це записується як `(s1: String, s2: String) -> Bool`. Однак, для виразів замикань, оголошених по місцю використання, параметри та значення, що повертається, записуються *всередині* фігурних дужок, а не поза ними.

Початок тіла замикання вводиться ключовим словом `in`. Це ключове слово розмежовує кінець оголошенню параметрів замикання та типу, що воно повертає, та початок тіла замикання.

Оскільки тіло цього замикання є досить коротке, його можна навіть записати в один рядок:

```swiftreversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```

Приклад вище ілюструє, що весь виклик методу `sorted(by:)` залишився без змін. Круглі дужки досі огортають весь аргумент цього методу. Однак, цей аргумент тепер є замиканням, оголошеним по місцю використання.
#### Визначення типу з контексту
Because the sorting closure is passed as an argument to a method, Swift can infer the types of its parameters and the type of the value it returns. The `sorted(by:)` method is being called on an array of strings, so its argument must be a function of type `(String, String) -> Bool`. This means that the `(String, String)` and `Bool` types do not need to be written as part of the closure expression’s definition. Because all of the types can be inferred, the return arrow (`->`) and the parentheses around the names of the parameters can also be omitted:

```swiftreversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```
It is always possible to infer the parameter types and return type when passing a closure to a function or method as an inline closure expression. As a result, you never need to write an inline closure in its fullest form when the closure is used as a function or method argument.
Nonetheless, you can still make the types explicit if you wish, and doing so is encouraged if it avoids ambiguity for readers of your code. In the case of the `sorted(by:)` method, the purpose of the closure is clear from the fact that sorting is taking place, and it is safe for a reader to assume that the closure is likely to be working with `String` values, because it is assisting with the sorting of an array of strings.
#### Implicit Returns from Single-Expression Closures
Single-expression closures can implicitly return the result of their single expression by omitting the `return` keyword from their declaration, as in this version of the previous example:

```swiftreversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```
Here, the function type of the `sorted(by:)` method’s argument makes it clear that a `Bool` value must be returned by the closure. Because the closure’s body contains a single expression (`s1 > s2`) that returns a `Bool` value, there is no ambiguity, and the `return` keyword can be omitted.
#### Shorthand Argument Names
Swift automatically provides shorthand argument names to inline closures, which can be used to refer to the values of the closure’s arguments by the names `$0`, `$1`, `$2`, and so on.
If you use these shorthand argument names within your closure expression, you can omit the closure’s argument list from its definition, and the number and type of the shorthand argument names will be inferred from the expected function type. The `in` keyword can also be omitted, because the closure expression is made up entirely of its body:

```swiftreversedNames = names.sorted(by: { $0 > $1 } )
```
Here, `$0` and `$1` refer to the closure’s first and second `String` arguments.
#### Operator Methods
There’s actually an even *shorter* way to write the closure expression above. Swift’s `String` type defines its string-specific implementation of the greater-than operator (`>`) as a method that has two parameters of type `String`, and returns a value of type `Bool`. This exactly matches the method type needed by the `sorted(by:)` method. Therefore, you can simply pass in the greater-than operator, and Swift will infer that you want to use its string-specific implementation:

```swiftreversedNames = names.sorted(by: >)
```
For more about operator method, see [Operator Methods](24_advanced_operators.md#operator-methods).
### Trailing Closures
If you need to pass a closure expression to a function as the function’s final argument and the closure expression is long, it can be useful to write it as a *trailing closure* instead. A trailing closure is written after the function call’s parentheses, even though it is still an argument to the function. When you use the trailing closure syntax, you don’t write the argument label for the closure as part of the function call.

```swiftfunc someFunctionThatTakesAClosure(closure: () -> Void) {    // function body goes here} // Here's how you call this function without using a trailing closure: someFunctionThatTakesAClosure(closure: {    // closure's body goes here}) // Here's how you call this function with a trailing closure instead: someFunctionThatTakesAClosure() {    // trailing closure's body goes here}
```
The string-sorting closure from the [Closure Expression Syntax](6_closures.md#closure-expression-syntax) section above can be written outside of the `sorted(by:)` method’s parentheses as a trailing closure:

```swiftreversedNames = names.sorted() { $0 > $1 }
```
If a closure expression is provided as the function or method’s only argument and you provide that expression as a trailing closure, you do not need to write a pair of parentheses `()` after the function or method’s name when you call the function:

```swiftreversedNames = names.sorted { $0 > $1 }
```
Trailing closures are most useful when the closure is sufficiently long that it is not possible to write it inline on a single line. As an example, Swift’s `Array` type has a `map(_:)` method which takes a closure expression as its single argument. The closure is called once for each item in the array, and returns an alternative mapped value (possibly of some other type) for that item. The nature of the mapping and the type of the returned value is left up to the closure to specify.
After applying the provided closure to each array element, the `map(_:)` method returns a new array containing all of the new mapped values, in the same order as their corresponding values in the original array.
Here’s how you can use the `map(_:)` method with a trailing closure to convert an array of `Int` values into an array of `String` values. The array `[16, 58, 510]` is used to create the new array `["OneSix", "FiveEight", "FiveOneZero"]`:

```swiftlet digitNames = [    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"]let numbers = [16, 58, 510]
```
The code above creates a dictionary of mappings between the integer digits and English-language versions of their names. It also defines an array of integers, ready to be converted into strings.
You can now use the `numbers` array to create an array of `String` values, by passing a closure expression to the array’s `map(_:)` method as a trailing closure:

```swiftlet strings = numbers.map {    (number) -> String in    var number = number    var output = ""    repeat {        output = digitNames[number % 10]! + output        number /= 10    } while number > 0    return output}// strings is inferred to be of type [String]// its value is ["OneSix", "FiveEight", "FiveOneZero"]
```
The `map(_:)` method calls the closure expression once for each item in the array. You do not need to specify the type of the closure’s input parameter, `number`, because the type can be inferred from the values in the array to be mapped.
In this example, the variable `number` is initialized with the value of the closure’s `number` parameter, so that the value can be modified within the closure body. (The parameters to functions and closures are always constants.) The closure expression also specifies a return type of `String`, to indicate the type that will be stored in the mapped output array.
The closure expression builds a string called `output` each time it is called. It calculates the last digit of `number` by using the remainder operator (`number % 10`), and uses this digit to look up an appropriate string in the `digitNames` dictionary. The closure can be used to create a string representation of any integer greater than zero.
> **Note**
> > The call to the `digitNames` dictionary’s subscript is followed by an exclamation mark (`!`), because dictionary subscripts return an optional value to indicate that the dictionary lookup can fail if the key does not exist. In the example above, it is guaranteed that `number % 10` will always be a valid subscript key for the `digitNames` dictionary, and so an exclamation mark is used to force-unwrap the `String` value stored in the subscript’s optional return value.
The string retrieved from the `digitNames` dictionary is added to the *front* of `output`, effectively building a string version of the number in reverse. (The expression `number % 10` gives a value of `6` for `16`, `8` for `58`, and `0` for `510`.)
The `number` variable is then divided by `10`. Because it is an integer, it is rounded down during the division, so `16` becomes `1`, `58` becomes `5`, and `510` becomes `51`.
The process is repeated until `number` is equal to `0`, at which point the `output` string is returned by the closure, and is added to the output array by the `map(_:)` method.
The use of trailing closure syntax in the example above neatly encapsulates the closure’s functionality immediately after the function that closure supports, without needing to wrap the entire closure within the `map(_:)` method’s outer parentheses.### Захоплення значень### Capturing Values
A closure can *capture* constants and variables from the surrounding context in which it is defined. The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.
In Swift, the simplest form of a closure that can capture values is a nested function, written within the body of another function. A nested function can capture any of its outer function’s arguments and can also capture any constants and variables defined within the outer function.
Here’s an example of a function called `makeIncrementer`, which contains a nested function called `incrementer`. The nested `incrementer()` function captures two values, `runningTotal` and `amount`, from its surrounding context. After capturing these values, `incrementer` is returned by `makeIncrementer` as a closure that increments `runningTotal` by `amount` each time it is called.

```swiftfunc makeIncrementer(forIncrement amount: Int) -> () -> Int {    var runningTotal = 0    func incrementer() -> Int {        runningTotal += amount        return runningTotal    }    return incrementer}
```
The return type of `makeIncrementer` is `() -> Int`. This means that it returns a *function*, rather than a simple value. The function it returns has no parameters, and returns an `Int` value each time it is called. To learn how functions can return other functions, see [Function Types as Return Types](5_functions.md#Function-Types-as-Return-Types).
The `makeIncrementer(forIncrement:)` function defines an integer variable called `runningTotal`, to store the current running total of the incrementer that will be returned. This variable is initialized with a value of `0`.
The `makeIncrementer(forIncrement:)` function has a single `Int` parameter with an argument label of `forIncrement`, and a parameter name of `amount`. The argument value passed to this parameter specifies how much `runningTotal` should be incremented by each time the returned incrementer function is called. The `makeIncrementer` function defines a nested function called `incrementer`, which performs the actual incrementing. This function simply adds `amount` to `runningTotal`, and returns the result.
When considered in isolation, the nested `incrementer()` function might seem unusual:

```swiftfunc incrementer() -> Int {    runningTotal += amount    return runningTotal}
```
The `incrementer()` function doesn’t have any parameters, and yet it refers to `runningTotal` and `amount` from within its function body. It does this by capturing a *reference* to `runningTotal` and `amount` from the surrounding function and using them within its own function body. Capturing by reference ensures that `runningTotal` and `amount` do not disappear when the call to `makeIncrementer` ends, and also ensures that `runningTotal` is available the next time the `incrementer` function is called.
> **Note**
> > As an optimization, Swift may instead capture and store a *copy* of a value if that value is not mutated by a closure, and if the value is not mutated after the closure is created.
> > Swift also handles all memory management involved in disposing of variables when they are no longer needed.
Here’s an example of `makeIncrementer` in action:

```swiftlet incrementByTen = makeIncrementer(forIncrement: 10)
```
This example sets a constant called `incrementByTen` to refer to an incrementer function that adds `10` to its `runningTotal` variable each time it is called. Calling the function multiple times shows this behavior in action:

```swiftincrementByTen()// returns a value of 10incrementByTen()// returns a value of 20incrementByTen()// returns a value of 30
```
If you create a second incrementer, it will have its own stored reference to a new, separate `runningTotal` variable:

```swiftlet incrementBySeven = makeIncrementer(forIncrement: 7)incrementBySeven()// returns a value of 7
```
Calling the original incrementer (`incrementByTen`) again continues to increment its own `runningTotal` variable, and does not affect the variable captured by `incrementBySeven`:

```swiftincrementByTen()// returns a value of 40
```
> **Note**
> > If you assign a closure to a property of a class instance, and the closure captures that instance by referring to the instance or its members, you will create a strong reference cycle between the closure and the instance. Swift uses capture lists to break these strong reference cycles. For more information, see [Strong Reference Cycles for Closures](15_automatic_reference_counting.md#Strong-Reference-Cycles-for-Closures).
 ### Closures Are Reference Types
In the example above, `incrementBySeven` and `incrementByTen` are constants, but the closures these constants refer to are still able to increment the `runningTotal` variables that they have captured. This is because functions and closures are *reference types*.
Whenever you assign a function or a closure to a constant or a variable, you are actually setting that constant or variable to be a *reference* to the function or closure. In the example above, it is the choice of closure that `incrementByTen` *refers* to that is constant, and not the contents of the closure itself.
This also means that if you assign a closure to two different constants or variables, both of those constants or variables will refer to the same closure:

```swiftlet alsoIncrementByTen = incrementByTenalsoIncrementByTen()// returns a value of 50
```
### Escaping Closures
A closure is said to *escape* a function when the closure is passed as an argument to the function, but is called after the function returns. When you declare a function that takes a closure as one of its parameters, you can write `@escaping` before the parameter’s type to indicate that the closure is allowed to escape.
One way that a closure can escape is by being stored in a variable that is defined outside the function. As an example, many functions that start an asynchronous operation take a closure argument as a completion handler. The function returns after it starts the operation, but the closure isn’t called until the operation is completed — the closure needs to escape, to be called later. For example:

```swiftvar completionHandlers: [() -> Void] = []func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {    completionHandlers.append(completionHandler)}
```
The `someFunctionWithEscapingClosure(_:)` function takes a closure as its argument and adds it to an array that’s declared outside the function. If you didn’t mark the parameter of this function with `@escaping`, you would get a compiler error.
Marking a closure with `@escaping` means you have to refer to `self` explicitly within the closure. For example, in the code below, the closure passed to `someFunctionWithEscapingClosure(_:)` is an escaping closure, which means it needs to refer to `self` explicitly. In contrast, the closure passed to `someFunctionWithNonescapingClosure(_:)` is a nonescaping closure, which means it can refer to `self` implicitly.

```swiftfunc someFunctionWithNonescapingClosure(closure: () -> Void) {    closure()} class SomeClass {    var x = 10    func doSomething() {        someFunctionWithEscapingClosure { self.x = 100 }        someFunctionWithNonescapingClosure { x = 200 }    }} let instance = SomeClass()instance.doSomething()print(instance.x)// Prints "200" completionHandlers.first?()print(instance.x)// Prints "100"
```
### Autoclosures
An *autoclosure* is a closure that is automatically created to wrap an expression that’s being passed as an argument to a function. It doesn’t take any arguments, and when it’s called, it returns the value of the expression that’s wrapped inside of it. This syntactic convenience lets you omit braces around a function’s parameter by writing a normal expression instead of an explicit closure.
It’s common to *call* functions that take autoclosures, but it’s not common to *implement* that kind of function. For example, the `assert(condition:message:file:line:)` function takes an autoclosure for its `condition` and `message` parameters; its condition parameter is evaluated only in debug builds and its `message` parameter is evaluated only if `condition` is `false`.
An autoclosure lets you delay evaluation, because the code inside isn’t run until you call the closure. Delaying evaluation is useful for code that has side effects or is computationally expensive, because it lets you control when that code is evaluated. The code below shows how a closure delays evaluation.

```swiftvar customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]print(customersInLine.count)// Prints "5" let customerProvider = { customersInLine.remove(at: 0) }print(customersInLine.count)// Prints "5" print("Now serving \(customerProvider())!")// Prints "Now serving Chris!"print(customersInLine.count)// Prints "4"
```
Even though the first element of the `customersInLine` array is removed by the code inside the closure, the array element isn’t removed until the closure is actually called. If the closure is never called, the expression inside the closure is never evaluated, which means the array element is never removed. Note that the type of `customerProvider` is not `String` but `() -> String` — a function with no parameters that returns a string.
You get the same behavior of delayed evaluation when you pass a closure as an argument to a function.

```swift// customersInLine is ["Alex", "Ewa", "Barry", "Daniella"]func serve(customer customerProvider: () -> String) {    print("Now serving \(customerProvider())!")}serve(customer: { customersInLine.remove(at: 0) } )// Prints "Now serving Alex!"
```
The `serve(customer:)` function in the listing above takes an explicit closure that returns a customer’s name. The version of `serve(customer:)` below performs the same operation but, instead of taking an explicit closure, it takes an autoclosure by marking its parameter’s type with the `@autoclosure` attribute. Now you can call the function as if it took a `String` argument instead of a closure. The argument is automatically converted to a closure, because the `customerProvider` parameter’s type is marked with the `@autoclosure` attribute.

```swift// customersInLine is ["Ewa", "Barry", "Daniella"]func serve(customer customerProvider: @autoclosure () -> String) {    print("Now serving \(customerProvider())!")}serve(customer: customersInLine.remove(at: 0))// Prints "Now serving Ewa!"
```
> **Note**
> > Overusing autoclosures can make your code hard to understand. The context and function name should make it clear that evaluation is being deferred.If you want an autoclosure that is allowed to escape, use both the `@autoclosure` and `@escaping` attributes. The `@escaping` attribute is described above in [Escaping Closures](6_closures.md#escaping-closures).

```swift// customersInLine is ["Barry", "Daniella"]var customerProviders: [() -> String] = []func collectCustomerProviders(_ customerProvider: @autoclosure @escaping () -> String) {    customerProviders.append(customerProvider)}collectCustomerProviders(customersInLine.remove(at: 0))collectCustomerProviders(customersInLine.remove(at: 0)) print("Collected \(customerProviders.count) closures.")// Prints "Collected 2 closures."for customerProvider in customerProviders {    print("Now serving \(customerProvider())!")}// Prints "Now serving Barry!"// Prints "Now serving Daniella!"
```
In the code above, instead of calling the closure passed to it as its `customerProvider` argument, the `collectCustomerProviders(_:)` function appends the closure to the `customerProviders` array. The array is declared outside the scope of the function, which means the closures in the array can be executed after the function returns. As a result, the value of the `customerProvider` argument must be allowed to escape the function’s scope.