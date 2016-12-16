## Основи

Мова Swift - це нова мова програмування для розробки додатків для iOS, macOS, watchOS, та tvOS. Проте багато частин Swift будуть знайомі з вашого досвіду розробки на мовах C та Objective-C.

Мова Swift надає свої власні версії всіх фундаментальних типів C та Objective-C, включаючи `Int` для цілих чисел, `Double` та `Float` для значень з плаваючою комою, `Bool` для Булевих значень, та `String` для текстової інформації. Мова Swift також надає потужні версії трьох основних типів колекцій: `Array`, `Set`, та `Dictionary`, як описано в [Колекціях](3_collection_types.md).

Як і мова C, мова Swift використовує зміння щоб зберігати значення та щоб посилатись на них по ідентифікатору. У мові Swift також широко вживаються змінні, чиє значення не може бути змінене. Вони відомі як константи, але вони набагато потужніші ніж константи в мові C. Константи вживаються всюди у Swift, щоб зробити код безпечнішим та більш ясним у намірах, коли ви працюєте зі значеннями, котрим не потрібно змінюватись. 

Окрім знайомих типів, у мові Swift з'являються більш розвинені типи, котрих нема в Objective-C, наприклад, кортежі. Кортежі дозволяють створювати та передавати групи значень. За допомогою кортежа можна повернути одразу декілька значень з функції як єдине об'єднане значення.

У мові Swift також вводяться опціональні типи - опціонали - які дозволяють обробляти відсутність значення. Опціонали виражають або "є деяке значення, і воно дорівнює x” або “немає взагалі жодного значення”. Користування опціоналами схоже на використання `nil` із вказівниками в Objective-C, але опціонали працюють з усіма типами, а не тільки з класами. Опціонали є не просто більш безпечніші та виразніші аніж вказівники на `nil` в Objective-C, вони лежать у серці найбільш потужних можливостей Swift.

Мова Swift типобезпечна, тобто мова допомагає вам виражатись ясно щодо типів значень, з якими  працює ваш код. Якщо частина вашого коду очікує `String`, типобезпечність не дасть вам помилково передати в нього `Int`. Подібним чином типобезпечність не дасть вам помилково передати опціональний `String` в частину коду, котра очікує неопціональний `String`. Типобезпечність дозволяє в процесі розробки відловлювати і виправляти помилки як можна раніше.

### Константи і змінні

Константи і змінні асоціюють ім'я (як, наприклад, `maximumNumberOfLoginAttempts` чи `welcomeMessage`) із значенням певного типу (такі як число `10` чи рядок `"Hello"`). Як тільки значення константи задано, воно не може бути змінене, тоді як значення змінної може бути змінене на інше в майбутньому.

#### Оголошення констант та змінних

Константи і змінні повинні бути оголошені до того, як вони будуть вжиті. Константи оголошуються за допомогою ключового слова `let`, а змінні - за допомогою ключового слова `var`. Ось приклад того, як константи і змінні можуть бути використані для того, щоб відслідковувати кількість спроб користувача увійти в систему.  

```swift
let maximumNumberOfLoginAttempts = 10var currentLoginAttempt = 0
```
Даний код можна прочитати так: 

“Оголошуємо нову константу під іменем `maximumNumberOfLoginAttempts` (максимальна кількість спроб увійти), і надаємо їх значення `10`. Потім оголошуємо нову змінну під іменем `currentLoginAttempt` (поточна кількість спроб увійти), і надаємо їй початкове значення `0`.”

У цьому прикладі максимальна кількість спроб увійти оголошено константою, тому що максимальна кількість спроб ніколи не зміниться. Поточна кількість спроб увійти оголошено змінною, бо це значення має збільшуватись на одиницю після кожної невдалої спроби користувача увійти в систему.

Ми можемо оголосити кілька констант чи змінних в один рядок, відділивши їх комами: ```swiftvar x = 0.0, y = 0.0, z = 0.0```> **Примітка**
> 
> Якщо значення, що зберігається у вашому коді, наврядчи зміниться, завжди оголошуйте його як константу за допомогою ключового слова `let`. Вживайте змінні тільки для зберігання значень, які реально повинні змінюватись.#### Анотації типів

Можна вживати анотації типів під час оголошення констант чи змінних, щоб було зрозуміло, який тип даних може зберігати константа чи змінна. Анотацію типу можна вказати, поставивши двокрапку після імені константи чи змінної, пробіл та ім'я бажаного типу.

У наступному прикладі ми надаємо анотацію типу змінній `welcomeMessage`, щоб позначити, що ця змінна може зберігати значення типу `String`:```swiftvar welcomeMessage: String
```
Двокрапка в оголошення означає “…що має тип…,” тобто код вище можна прочитати так:

“Оголошуємо змінну з іменем `welcomeMessage` що має тип `String`.”

Фраза “що має тип `String`” означає “може зберігати будь-які значення типу `String`.” Це слід розуміти як “тип речі” (чи “вид речі”) що може зберігатись.Тепер змінній `welcomeMessage` можна присвоїти будь-яке рядкове значення без помилок:

```swiftwelcomeMessage = "Hello"
```

Можна оголосити кілька пов'язаних змінних одного типу в один рядок, відділивши їх імена комами, та вказавши єдину анотацію типу після останнього імені змінної:

```swiftvar red, green, blue: Double
```> **Примітка**
> 
> На практиці анотаціями типів доводиться користуватись рідко. Якщо надати початкове значення константі чи змінній в момент оголошення, мова Swift майже завжди може визначити тип, який повинна мати дана константа чи змінна. Це більш детально описано в [Типобезпечність та Визначення Типів](#типобезпечність-та-визначення-типів). У прикладі вище в оголошенні `welcomeMessage` не вказано початкове значення, тому тип змінної `welcomeMessage` визначається анотацією типу. 

#### Іменування констант і зміннихІмена констант і змінних можуть містити майже будь-які символи, в тому числі символи Unicode:

```swiftlet π = 3.14159let 你好 = "你好世界"let 🐶🐮 = "dogcow"
```Імена констант та змінних не можуть містити пробільних символів, математичних символів, стрілок, приватні (чи недійсні) коди Unicode, символи для малювання ліній та рамок. Змінні також не можуть починатись з цифри, хоча цифри можуть бути входити в ім'я в будь-якому іншому місці. Як тильки було оголошено константу чи змінну певного типу, неможливо переоголосити її з таким же ім'ям, або тип. Так само неможливо зробити константу змінною чи навпаки.> **Примітка**>
> Якщо потрібно дати константі чи змінній ім'я, що співпадає з зарезервованим мовою Swift ключовим словом, можна заключити ім'я в косі апострофи (`` ` ``). Однак не бажано вживати ключові слова як імена констант чи змінних, окрім видадків коли не зовсім немає іншого вибору. 

Значення змінної можна змінити на інше значення сумісного типу. В наступному прикладі ми змінимо значення змінної `friendlyWelcome` з `"Hello!"` на `"Вітаю!"`:

```swiftvar friendlyWelcome = "Hello!"friendlyWelcome = "Вітаю!"// змінна friendlyWelcome стала тепер "Вітаю!"
```Навідміну від змінних, як тільки значення константи задано - його неможливо змінити. Спроба зміни значення виллється в помилку компіляції:
```swiftlet languageName = "Swift"languageName = "Swift++"// Це помилка часу компіляції: languageName не може бути змінено.```

#### Друк констант та зміннихМожна надрукувати поточне значення константи чи змінної за допомогою функції `print(_:separator:terminator:)`:```swiftprint(friendlyWelcome)// Надрукує "Вітаю!"
``` 
Функція `print(_:separator:terminator:)` є глобальною функцією, що друкує одне або кілька значень у відповідний вивід. У Xcode, наприклад, функція `print(_:separator:terminator:)` друкує у "консольну" панель. Параметри  `separator` (символ-розділювач) та `terminator` (символ-закінчення) мають значення за замовчуванням, тому їх можна пропустити під час виклику функції. За замовчуванням, функція закінчує рядок, що друкує, символом переходу на новий рядок. Щоб вивести значення без переходу на новий рядок у кінці, можна передати порожній рядок в якості параметра `terminator`. Наприклад, `print(someValue, terminator: "")`. Для більш детальної інформації про параметри із значенням за замовчуванням, дивіться [Значення параметрів за замовчуванням](1_language_guide/5_functions.md#значення-параметрів-за-замовчуванням).

У мові Swift є механізм *інтерполяції рядків*, що дозволяє включити і'мя константи чи змінної у більш довгий рядок як заповнювач, що буде замінено на поточне значення константи чи змінної. Для цього потрібно огорнути ім'я у круглі дужки, поставивши перед дужкою, що відкривається, 
Swift uses *string interpolation* to include the name of a constant or variable as a placeholder in a longer string, and to prompt Swift to replace it with the current value of that constant or variable. Wrap the name in parentheses and escape it with a зворотній слеш `\`:

```swiftprint("The current value of friendlyWelcome is \(friendlyWelcome)")// Надрукує "The current value of friendlyWelcome is Вітаю!"
```
> **Note**> 
> Детальніше ознайомитись з можливостями інтерполяції рядків можна у розділі [Інтерполяція рядків](1_language_guide/2_strings_and_characters.md#iнтерполяція-рядків)
### Коментарі

Коментарі - це блоки тексту у коді, що не впливають на виконнання коду. Їх вживають як примітки чи нагадування для себе. Коментарі ігноруються компілятором Swift. 

Коментарі у мові Swift дуже схожі на коментарі в мові C. Однорядкові коментарі починаються з подвійного прямого слеша (`//`):

```swift
// Це коментар.
```

Багаторядкові коментарі починаються із символів слешу та зірочки (`/*`) і закінчуються символами зірочки та слешу (`*/`):

```swift
/* Це також коментар,
 але написаний у кілька рядків. */
```

Навідміну від коментарів у мові C, багаторядкові коментарі в мові Swift можуть бути вкладені в інші багаторядкові коментарі. Щоб написати вкладені коментарі, слід просто розпочати блок багаторядкових коментарів, а потім розпочати ще один блок багаторядкових коментарів усередині першого блоку. Потім слід закрити спочатку вкладений блок коментарів, а потім перший блок: 

```swift
/* Це початок першого багаторядкового коментаря. /* Це другий, вкладений багаторядковий коментар. */
 Це кінець першого багаторядкового коментаря. */
```Вкладені багаторядкові коментарі дозволяють закоментувати великі блоки коду швидко і легко, навіть якщо код уже містить багаторядкові коментарі.

### Крапка з комою

Навідміну від багатьох інших мов, у мові Swift не вимагається ставити крапку з комою (`;`) після кожної інструкції у коді, хоча її і можна ставити за бажанням.  
Однак крапку з комою ставити *обов'язково* якщо потрібно написати кілька окремих інструкцій в один рядок:

```swift
let cat = "🐱"; print(cat)// Друкує "🐱"
```

### Цілі числа
*Цілими числами* є числа без дробової частини, такі як `42` та `-23`. Цілі числа бувають або *знаковими* (додатні, від'ємні та нуль), або *беззнаковими* (додатні та нуль).

У мові Swift знакові та беззнакові цілі можна зберігати у 8-, 16-, 32-, та 64-бітній формах. Назви типів цілих відповідають нормам кодування, схожим на відповідні норми в мові С: 8-бітний беззнаковий цілий тим має назву `UInt8`, а 32-бітний знаковий цілий тип має назву `Int32`. Як і всі інші типи у мові Swift, цілі типи мають імена, що пишуться у [ВерхньомуВерблюжомуРегістрі](https://uk.wikipedia.org/wiki/Верблюжий_регістр).

#### Межі цілих чисел

Доступитись до найбільшого і найменшого можливого значення кожного з цілих типів можна за властивостями `min` та `max`:
```swift
let minValue = UInt8.min  // minValue дорівнює 0, і має тип UInt8let maxValue = UInt8.max  // maxValue дорівнює 255, і має тип UInt8
```

Значення цих властивостей мають числовий тип відповідного розміру (такий як `UInt8` у прикладі вище), і можуть далі використовуватись у виразах разом із іншими значеннями того ж типу. 
#### Int

У більшості випадків не потрібно обирати конкретний розмір цілочисельного типу. Мова Swift надає додатковий цілочислельний тип `Int`, що має такий же розмір, що і розмір машинного слова на поточній платформі. 
  + На 32-бітній платформі, тип `Int` має тикий же розмір, що і `Int32`. 
 + На 64-бітній платформі, тип `Int` має тикий же розмір, що і `Int64`. 

Окрім випадків, де потрібно працювати з конкретним розміром цілочисельного типу, слід користуватись типом `Int` для цілих значень у коді. Це допомагає коду бути консистентним і сумісним. Навіть на 32-бітній платформі, тип `Int` може зберігати значення від  `-2 147 483 648` до `2 147 483 647`, що є більш ніж достатньо для багатьох цілочислельних діапазонів. #### UInt

Мова Swift також надає беззнаковий цілочисельний тип `UInt`, що має такий же розмір, що і розмір машинного слова на поточній платформі:
 + На 32-бітній платформі, тип `UInt` має тикий же розмір, що і `UInt32`. 
 + На 64-бітній платформі, тип `UInt` має тикий же розмір, що і `UInt64`. 
 
> **Примітка**
> 
> Слід уживати `UInt` тільки тоді, коли конкретно потрібен беззнаковий цілочисельний тип розміру, що співпадає з розміром машинного слова поточної платформи. Якщо це не ваш випадок, слід надавати перевагу типові `Int`, навіть якщо значення, що буде зберігатись, точно не може бути від'ємним. Послідовне вживання типу `Int` для цілих значень допомагає коду бути сумісним, оминати необхідність постійно конвертувати один числовий тип у інший, і відповідає цілочисельному визначенню типів, як описано у розділі [Типобезпечність та Визначення Типів](#типобезпечність-та-визначення-типів).
 
#### Числа з рухомою комою

Числами з рухомою комою є числа з дробовою частино, такі як `3.14159`, `0.1`, та `-273.15`.Числа з рухомою комою можуть представити набагато більший діапазон значень, ніж цілочисельні типи, і може зберігати числа, що набагато більші чи менші ніж ті, що можуть зберігатись у типі `Int`. Мова Swift надає два знакових типи для числе з рухомою комою:  
 + `Double` представляє 64-бітні числа з рухомою комою. + `Float` представляє 32-бітні числа з рухомою комою.
 > **Примітка**> 
> Тип `Double` має точнісь у як мінімум 15 десяткових цифр, тоді як точність типу `Float` може бути всього лише 6 десяткових цифр. Доречний вибір типу чисел з рухомою комою залежить від природи і діапазону значень, з якими потрібно працювати у коді. У ситуаціях коли обидва типи можуть бути доречними, слід надавати перевагу типу `Double`.
#### Типобезпечність та Визначення Типів

Мова Swift - типобезбечна. Типобезпечна мова заохочує розробників бути ясними щодо типів значень, з якими може працювати їх код. Якщо частина коду очікує рядок (`String`), неможливо помилково передати в нього число (`Int`). 

Оскільки мова Swift - типобезпечна, перевірка типів відбувається під час компіляції коду, і несумісні типи сигналізуються помилками. Це дозволяє відловлювати і виправляти помилки в процесі розробки на стільки рано, на скільки це можливо.

Перевірка типів допомагає уникати помилок під час роботи з різними типами значень. Однка це не означає, що потрібно вказувати тип кожної константи та змінної, що оголошується. Якщо тип потрібного значення не вказано, мова Swift вираховує потрібний тип за допомогою механізму *визначення типів*. Визначення типів дозволяє компілятору вивести тип певного виразу автоматично під час компіляції коду, просто вивчивши надані вами значення.

Через визначення типів мова Swift вимагає набагато меншої кількості оголошень типів, аніж інші мови, такі як C чи Objective-C. Константи та змінні є все ще явно типізовані, але більша частина роботи по вказанню типу робиться за вас. 

Зокрема, визначення типів є корисним під час оголошень констант чи змінних із вказанням початкового значення. Це часто робиться через присвоєння *літерального значення* (або *літералу*) константі чи змінній під час її оголошення. (Літеральним значенням називають значення, що з'являється у коді прямо, наприклад числа `42` та `3.14159` у прикладах нижче.)

Наприклад, якщо присвоїти літеральне значення `42` новій костанті і не вказати, якого вона типу, мова Swift визначить, що константа повинна мати тип `Int`, бо вона ініціалізована числом, що схоже на ціле:
```swiftlet meaningOfLife = 42// визначено, що meaningOfLife матиме тип Int
```

Аналогічно, якщо не вказано тип для літералу з рухомою комою, Swift визначить, що тут був намір створити `Double`:

```swiftlet pi = 3.14159// визначено, що pi матиме тип Double
```

Swift завжди обирає `Double` (а не `Float`) під час визначення типу числа з рухомою комою.

Якщо поєднати цілочисельний літерал з літералом з рухомою комою у виразі, з контексту буде визначено тип `Double`:```swiftlet anotherPi = 3 + 0.14159// anotherPi також визначається як значення типу Double
```

Літеральне значення `3` не має явного типу саме по собі, і тому відповідний вихідний тип `Double` визначено з присутності літералу з рухомою комою в частині виразу.#### Numeric LiteralsInteger literals can be written as:
 + A decimal number, with no prefix + A binary number, with a 0b prefix + An octal number, with a 0o prefix + A hexadecimal number, with a 0x prefix
	All of these integer literals have a decimal value of `17`:

```swiftlet decimalInteger = 17let binaryInteger = 0b10001       // 17 in binary notationlet octalInteger = 0o21           // 17 in octal notationlet hexadecimalInteger = 0x11     // 17 in hexadecimal notation
```Floating-point literals can be decimal (with no prefix), or hexadecimal (with a `0x` prefix). They must always have a number (or hexadecimal number) on both sides of the decimal point. Decimal floats can also have an optional exponent, indicated by an uppercase or lowercase `e`; hexadecimal floats must have an exponent, indicated by an uppercase or lowercase `p`.
For decimal numbers with an exponent of `exp`, the base number is multiplied by 10<sup>exp</sup>:
 `1.25e2` means 1.25 x 10<sup>2</sup>, or `125.0`.
 
 `1.25e-2` means 1.25 x 10<sup>-2</sup>, or `0.0125`.
 For hexadecimal numbers with an exponent of exp, the base number is multiplied by 2<sup>exp</sup>:
 `0xFp2` means 15 x 2<sup>2</sup>, or 60.0.
  `0xFp-2` means 15 x 2<sup>-2</sup>, or 3.75.
 All of these floating-point literals have a decimal value of `12.1875`:
```swift
let decimalDouble = 12.1875let exponentDouble = 1.21875e1let hexadecimalDouble = 0xC.3p0
```
Numeric literals can contain extra formatting to make them easier to read. Both integers and floats can be padded with extra zeros and can contain underscores to help with readability. Neither type of formatting affects the underlying value of the literal:

```swiftlet paddedDouble = 000123.456let oneMillion = 1_000_000let justOverOneMillion = 1_000_000.000_000_1
```

#### Numeric Type Conversion
Use the `Int` type for all general-purpose integer constants and variables in your code, even if they are known to be non-negative. Using the default integer type in everyday situations means that integer constants and variables are immediately interoperable in your code and will match the inferred type for integer literal values.
Use other integer types only when they are specifically needed for the task at hand, because of explicitly-sized data from an external source, or for performance, memory usage, or other necessary optimization. Using explicitly-sized types in these situations helps to catch any accidental value overflows and implicitly documents the nature of the data being used.
##### Integer Conversion
The range of numbers that can be stored in an integer constant or variable is different for each numeric type. An `Int8` constant or variable can store numbers between `-128` and `127`, whereas a `UInt8` constant or variable can store numbers between `0` and `255`. A number that will not fit into a constant or variable of a sized integer type is reported as an error when your code is compiled:

```swiftlet cannotBeNegative: UInt8 = -1// UInt8 cannot store negative numbers, and so this will report an errorlet tooBig: Int8 = Int8.max + 1// Int8 cannot store a number larger than its maximum value,// and so this will also report an error
```
Because each numeric type can store a different range of values, you must opt in to numeric type conversion on a case-by-case basis. This opt-in approach prevents hidden conversion errors and helps make type conversion intentions explicit in your code.
To convert one specific number type to another, you initialize a new number of the desired type with the existing value. In the example below, the constant twoThousand is of type `UInt16`, whereas the constant one is of type `UInt8`. They cannot be added together directly, because they are not of the same type. Instead, this example calls `UInt16(one)` to create a new `UInt16` initialized with the value of one, and uses this value in place of the original:

```swiftlet twoThousand: UInt16 = 2_000let one: UInt8 = 1let twoThousandAndOne = twoThousand + UInt16(one)
```
Because both sides of the addition are now of type `UInt16`, the addition is allowed. The output constant (`twoThousandAndOne`) is inferred to be of type `UInt16`, because it is the sum of two `UInt16` values.
`SomeType(ofInitialValue)` is the default way to call the initializer of a Swift type and pass in an initial value. Behind the scenes, `UInt16` has an initializer that accepts a `UInt8` value, and so this initializer is used to make a new `UInt16` from an existing `UInt8`. You can’t pass in any type here, however—it has to be a type for which `UInt16` provides an initializer. Extending existing types to provide initializers that accept new types (including your own type definitions) is covered in [Extensions](1_language_guide/20_extensions.md).

##### Integer and Floating-Point Conversion
Conversions between integer and floating-point numeric types must be made explicit:

```swiftlet three = 3let pointOneFourOneFiveNine = 0.14159let pi = Double(three) + pointOneFourOneFiveNine// pi equals 3.14159, and is inferred to be of type Double```

Here, the value of the constant `three` is used to create a new value of type `Double`, so that both sides of the addition are of the same type. Without this conversion in place, the addition would not be allowed.
Floating-point to integer conversion must also be made explicit. An integer type can be initialized with a `Double` or `Float` value:

```swiftlet integerPi = Int(pi)// integerPi equals 3, and is inferred to be of type Int
```
Floating-point values are always truncated when used to initialize a new integer value in this way. This means that `4.75` becomes `4`, and `-3.9` becomes `-3`.> Note>
> The rules for combining numeric constants and variables are different from the rules for numeric literals. The literal value 3 can be added directly to the literal value `0.14159`, because number literals do not have an explicit type in and of themselves. Their type is inferred only at the point that they are evaluated by the compiler.
#### Type Aliases
*Type aliases* define an alternative name for an existing type. You define type aliases with the typealias `keyword`.
Type aliases are useful when you want to refer to an existing type by a name that is contextually more appropriate, such as when working with data of a specific size from an external source:

```swifttypealias AudioSample = UInt16
```
Once you define a type alias, you can use the alias anywhere you might use the original name:

```swiftvar maxAmplitudeFound = AudioSample.min// maxAmplitudeFound is now 0
```

Here, `AudioSample` is defined as an alias for `UInt16`. Because it is an alias, the call to `AudioSample.min` actually calls `UInt16.min`, which provides an initial value of `0` for the `maxAmplitudeFound` variable.#### Booleans
Swift has a basic *Boolean* type, called `Bool`. Boolean values are referred to as *logical*, because they can only ever be true or false. Swift provides two Boolean constant values, `true` and `false`:

```swiftlet orangesAreOrange = truelet turnipsAreDelicious = false
```
The types of `orangesAreOrange` and `turnipsAreDelicious` have been inferred as `Bool` from the fact that they were initialized with Boolean literal values. As with `Int` and `Double` above, you don’t need to declare constants or variables as `Bool` if you set them to `true` or `false` as soon as you create them. Type inference helps make Swift code more concise and readable when it initializes constants or variables with other values whose type is already known.
Boolean values are particularly useful when you work with conditional statements such as the `if` statement:

```swiftif turnipsAreDelicious {    print("Mmm, tasty turnips!")} else {    print("Eww, turnips are horrible.")}// Prints "Eww, turnips are horrible."
```
Conditional statements such as the if statement are covered in more detail in [Control Flow](1_language_guide/4_control_flow.md).Swift’s type safety prevents non-Boolean values from being substituted for `Bool`. The following example reports a compile-time error:

```swiftlet i = 1if i {    // this example will not compile, and will report an error}
```
However, the alternative example below is valid:

```swiftlet i = 1if i == 1 {    // this example will compile successfully}
```
The result of the `i == 1` comparison is of type `Bool`, and so this second example passes the type-check. Comparisons like `i == 1` are discussed in [Basic Operators](1_language_guide/1_base_operators.md).As with other examples of type safety in Swift, this approach avoids accidental errors and ensures that the intention of a particular section of code is always clear.

####Tuples
*Tuples* group multiple values into a single compound value. The values within a tuple can be of any type and do not have to be of the same type as each other.In this example, `(404, "Not Found")` is a tuple that describes an HTTP *status code*. An HTTP status code is a special value returned by a web server whenever you request a web page. A status code of `404 Not Found` is returned if you request a webpage that doesn’t exist.

```swiftlet http404Error = (404, "Not Found")// http404Error is of type (Int, String), and equals (404, "Not Found")
```
The `(404, "Not Found")` tuple groups together an `Int` and a `String` to give the HTTP status code two separate values: a number and a human-readable description. It can be described as “a tuple of type `(Int, String)`”.You can create tuples from any permutation of types, and they can contain as many different types as you like. There’s nothing stopping you from having a tuple of type `(Int, Int, Int)`, or `(String, Bool)`, or indeed any other permutation you require.
You can *decompose* a tuple’s contents into separate constants or variables, which you then access as usual:```swiftlet (statusCode, statusMessage) = http404Errorprint("The status code is \(statusCode)")// Prints "The status code is 404"print("The status message is \(statusMessage)")// Prints "The status message is Not Found"
```
If you only need some of the tuple’s values, ignore parts of the tuple with an underscore (`_`) when you decompose the tuple:

```swiftlet (justTheStatusCode, _) = http404Errorprint("The status code is \(justTheStatusCode)")// Prints "The status code is 404"
```
Alternatively, access the individual element values in a tuple using index numbers starting at zero:

```swiftprint("The status code is \(http404Error.0)")// Prints "The status code is 404"print("The status message is \(http404Error.1)")// Prints "The status message is Not Found"
```
You can name the individual elements in a tuple when the tuple is defined:

```swiftlet http200Status = (statusCode: 200, description: "OK")If you name the elements in a tuple, you can use the element names to access the values of those elements:print("The status code is \(http200Status.statusCode)")// Prints "The status code is 200"print("The status message is \(http200Status.description)")// Prints "The status message is OK"
```
Tuples are particularly useful as the return values of functions. A function that tries to retrieve a web page might return the `(Int, String)` tuple type to describe the success or failure of the page retrieval. By returning a tuple with two distinct values, each of a different type, the function provides more useful information about its outcome than if it could only return a single value of a single type. For more information, see Functions with Multiple Return Values.

> **Note**
> 
> Tuples are useful for temporary groups of related values. They are not suited to the creation of complex data structures. If your data structure is likely to persist beyond a temporary scope, model it as a class or structure, rather than as a tuple. For more information, see [Classes and Structures](1_language_guide/8_classes_and_structures.md).

