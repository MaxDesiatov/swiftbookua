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
 
### Числа з рухомою комою

Числами з рухомою комою є числа з дробовою частино, такі як `3.14159`, `0.1`, та `-273.15`.Числа з рухомою комою можуть представити набагато більший діапазон значень, ніж цілочисельні типи, і може зберігати числа, що набагато більші чи менші ніж ті, що можуть зберігатись у типі `Int`. Мова Swift надає два знакових типи для числе з рухомою комою:  
 + `Double` представляє 64-бітні числа з рухомою комою. + `Float` представляє 32-бітні числа з рухомою комою.
 > **Примітка**> 
> Тип `Double` має точнісь у як мінімум 15 десяткових цифр, тоді як точність типу `Float` може бути всього лише 6 десяткових цифр. Доречний вибір типу чисел з рухомою комою залежить від природи і діапазону значень, з якими потрібно працювати у коді. У ситуаціях коли обидва типи можуть бути доречними, слід надавати перевагу типу `Double`.
### Типобезпечність та Визначення Типів

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

Літеральне значення `3` не має явного типу саме по собі, і тому відповідний вихідний тип `Double` визначено з присутності літералу з рухомою комою в частині виразу.### Числові літералиЦілочисельні літерали можуть бути записані як: 
 + Десяткове число, без префіксу + Двійкове число, з префіксом `0b` + Вісімкове число, з префіксом `0o` + Шістнадцяткове число, з префіксом `0x`


Усі наступні літерали мають десяткове значення `17`:

```swiftlet decimalInteger = 17let binaryInteger = 0b10001       // 17 в двійковій нотаціїlet octalInteger = 0o21           // 17 у вісімковій нотаціїlet hexadecimalInteger = 0x11     // 17 в шістнадцятковій нотації
```Літерали з рухомою комою межуть бути десятковими (без префіксу), або шістнадцятковими (з префіксом `0x`). Для них завжди повинно бути вказано десяткове (або шістнадцяткове) число по обидва боки від десяткового розділювача,  в якості якого вживається крапка. Десяткові літерали з рухомою комою можуть також мати **необов'язковий** показний ступеня, маркований прописною чи строковою `e`; шістнадцяткові літерали з рухомою комою **обов'язково** повинні мати показник ступеня, маркований прописною чи строковою `p`.

Для десяткових чисел з показником ступеня `exp`, мантиса множиться на 10<sup>exp</sup>:
 `1.25e2` означає 1.25 x 10<sup>2</sup>, або `125.0`.
 
 `1.25e-2` означає 1.25 x 10<sup>-2</sup>, або `0.0125`.
 
Для шістнадцяткових чисел з показником ступеня `exp`, мантиса множиться на 2<sup>exp</sup>:   `0xFp2` означає 15 x 2<sup>2</sup>, або 60.0.
   `0xFp-2` означає 15 x 2<sup>-2</sup>, або 3.75.

Усі наступні літерали з рухомою комою мають десяткове значення `12.1875`: 
```swift
let decimalDouble = 12.1875let exponentDouble = 1.21875e1let hexadecimalDouble = 0xC.3p0
```

Числові літерали можуть містити додаткове форматування, що їх було легше читати. 
І цілочисельні літерали, і літерали з рухомою комою можуть містити незначущі нулі, або містити символи підкреслення (`_`), щоб полегнити їх сприйняття. Жоден вид форматування не впливає на значення літералу: 

```swiftlet paddedDouble = 000123.456let oneMillion = 1_000_000let justOverOneMillion = 1_000_000.000_000_1
```

### Перетворення числових типів

Слід вживати тип `Int` для всіх цілочисельних констант і змінних загального призначення, навіть якщо відомо, що вони точно додатні. Вживаючи цілочисельний тип за замовчуванням в щоденних ситуаціях ми отримуємо константи і змінні, які є одразу сумісні у коді і підходять до типу, що виводиться з цілочисельних літеральних значень. 

Слід користуватись іншими цілочисельними типами тільки тоді, коли для задачі  потрібні конкретно сами вони. Наприклад, для обробки даних явного розміру із зовнішнього джерела, або для оптимізації швидкодії, пам'яті чи іншої необхідної оптимізації. Користування типами явного розміру у цих ситуаціях допомагає відловити будь-які несподівані переповнення значень і неявно документує природу інформації, яка використовується. 
#### Перетворення цілих чисел

Діапазон чисел, що можуть зберігатись у цілочисельній константі чи змінній є різним для кожного чисельного типу. Константа чи змінна типу `Int8` може зберігати значенням між `-128` та `127`, тоді як константа чи змінна типу `UInt8` може зберігати значенням між `0` та `255`. Якщо число не вміщується в розмір цілочисельного типу константи чи змінної, під час компіляції коду буде повідомлено про помилку:

```swiftlet cannotBeNegative: UInt8 = -1// UInt8 не може зберігати від'ємні числа,
// і тому це призведе до помилки компіляції
let tooBig: Int8 = Int8.max + 1// Int8 не може зберігати число, більше за максимальне значення,// і тому це призведе до помилки компіляції
```

Оскільки кожен числовий тип може зберігати різний діапазон значень, слід робити перетворення числових типів у кожному випадку окремо. Цей підхід захичає від помилок прихованих перетворень, і допомагає робити наміри перетворення типів у коді явними. 

Щоб перетворити одним конкретний числовий тип на інший, слід проініціалізувати нове число потрібного типу існуючим значенням. У наступному прикладі, константа  `twoThousand` має тип `UInt16`, тоді як константа `one` має тип `UInt8`. Їх не можна додавати прямо, бо вони різних типів. Замість цього, у прикладі викликається `UInt16(one)` щоб створити нове число типу `UInt16`, проініціалізоване значенням `one`, і це значення використовується замість початкового:

```swiftlet twoThousand: UInt16 = 2_000let one: UInt8 = 1let twoThousandAndOne = twoThousand + UInt16(one)
```

Оскільки обидва доданки тепер мають тип `UInt16`, додавання дозволяється. Тип вихідної константи (`twoThousandAndOne`) визначається як `UInt16`, бо це суми двох значень типу `UInt16`.

Вираз виду `ЯкийсьТип(зЯкимосьПочатковимЗначенням)` є звичайним способом виклакати ініціалізатор типу у Swift, і передати йому початкове значення. 
За лаштунками, тип `UInt16` має ініціалізатор, що приймає значення типу `UInt8`, і тому цей ініціалізатор вживається для створення нового значення типу `UInt16` з існуючого значення типу `UInt8`. Сюди не можна передати будь-яке значення, це має бути такий тип, для якого у `UInt16` є ініціалізатор. Однак у мові Swift є можливість розширити існуючий тип, додавши до нього новий ініціалізатор, що приймає новий тип (включаючи користувацький тип). Детальніше про це можна прочитати у розділі [Розширення](1_language_guide/20_extensions.md).

#### Перетворення цілих чисел та чисел з рухомою комою

Перетворення між цілочисельними числовими типами та типами з рухомою комою має відбуватись явно:
```swiftlet three = 3let pointOneFourOneFiveNine = 0.14159let pi = Double(three) + pointOneFourOneFiveNine// константа pi дорівнює 3.14159, і її тип визначено як Double```

Тут значення константи `three` використано для того, щоб створити нове значення типу `Double`, і тому обидва доданки мають однаковий тип. Якби це перетворення не мало місця, додавання не було б дозволено.

Перетворення чисел з рухомою комою на цілі також має бути явним. Ціле число можна проініціалізувати значенням типу `Double` чи `Float`:

```swiftlet integerPi = Int(pi)// константа integerPi дорівнює 3, і її тип визначено як Int
```

Значення з рухомою комою завжди усікаються під час ініціалізації цілих значень таким чином. Тобто `4.75` стане `4`, і `-3.9` стане `-3`.> **Примітка**>
> Правила поєднання числових констант і змінних відрізняються від правил для числових літералів. Літеральне значення `3` може бути додане прямо до літерального значення `0.14159`, бо числові літерали не мають явного типу самі по собі. Їх тип визначається тільки в момент, коли вони оцінюються компілятором.  
### Псевдоніми типів

*Псевдоніми типів* визначають альтернативне ім'я для існуючого типу. Псевдоніми типів визначаються за допомогою ключового слова `typealias`.

Псевдоніми типів корисні, коли потрібно посилатись на існуючий тип за іменем, що більш доречне в даному контексті. Наприклад, при роботі з інформацією фіксованого розміру із зовнішнього джерела:

```swifttypealias AudioSample = UInt16
```

Як тільки було оголошено псевдонім типу, його можна використовувати будь-де замість початкового імені: 
```swiftvar maxAmplitudeFound = AudioSample.min// maxAmplitudeFound тепер дорівнює 0
```

Тут `AudioSample` визначено як псевдонім до типу `UInt16`. Оскільки це псевдонім, виклик `AudioSample.min` насправді викликає `UInt16.min`, котрий надає початкове значення `0` змінній `maxAmplitudeFound`.### Булевий тип даних

Мова Swift має базовий *булевий* тип, що називається `Bool`. Булеві значення ще називають *логічними*, бо вони можуть бути лише істиною чи хибною. Мова Swift надає два булевих константних значення, `true` (істина) та `false` (хиба):


```swiftlet orangesAreOrange = truelet turnipsAreDelicious = false
```

Типи констант `orangesAreOrange` та `turnipsAreDelicious` було визначено як `Bool` через те, що їх було проініціалізовано булевими літералами. Так само як і  з типами `Int` та `Double` вище, не потрібно явно вказувати тип `Bool` якщо їм присвоюється значення `true` чи `false` одразу після створення. Визначення типів дозволяє робити код мовою Swift більш коротким та читабельним під час ініціалізації констант чи змінних значеннями, чий тип відомо. 

Булеві значення зокрема корисні під час роботи з умовними інструкціями, такими як інструкція `if`:

```swiftif turnipsAreDelicious {    print("Mmm, tasty turnips!")} else {    print("Eww, turnips are horrible.")}// Надрукує "Eww, turnips are horrible."
```

Умовні інструкції, такі як інструкція `if` описані більш детально у розділі  [Потік керування](4_control_flow.md).

Типобезпечність мови Swift запобігає підстановці небулевих значеня замість булевих. Наступний приклад призведе до повідомлення про помилку компіляції: 

```swiftlet i = 1if i {    // Цей приклад не скомпілюється, і буде повідомлено про помилку.}
```

Однак, альтернативний приклад нижче є дійсним: 

```swiftlet i = 1if i == 1 {    // Цей приклад успішно скомпілюється}
```

Результат порівняння `i == 1` має тип `Bool`, і тому другий приклад проходить перевірку типу. Порівняння на кшталт `i == 1` описано у розділі [Базові оператори](1_language_guide/1_base_operators.md).

Як і в інших прикладах типобезпечності у мові Swift, цей підхід запобігає випадковим помилкам і гарантує, що намір у окремій секції коду є завжди зрозумілим.

### Кортежі

*Кортежі* групують кілька значень в єдине складене значення. Значення всередині кортежу можуть бути будь-якого типу і не обов'язково повинні мати однаковий тип.  У наступному прикладі, `(404, "Not Found")` є кортежом, що описує *код cтану* HTTP. [Код стану HTTP](https://uk.wikipedia.org/wiki/Список_кодів_стану_HTTP) - це спеціальне значення, що повертається веб-сервером після кожного запиту веб-сторінки. Код стану `404 Not Found` повертається тоді, коли запитана сторінка не існує.

```swiftlet http404Error = (404, "Не знайдено")// http404Error має тип (Int, String), і дорівнює (404, "Не знайдено")
```

Кортеж `(404, "Not Found")` групує разом значення типів `Int` та `String` щоб надати коду стану HTTP два окремих значення: число і зручний для сприйняття людиною опис. Його можна описати як “кортеж типу `(Int, String)`”.Можна створити кортежі з будь-якої перестановки типів, і вони можуть містити скільки завгодно різних типів. Ніщо не заважає мати кортеж типу `(Int, Int, Int)` або `(String, Bool)`, або будь-яку іншу необхідну перестановку типів. 

Можна *розкласти* вміст кортежу на окремі константи чи змінні, до яких можна звертатись як звичайно:```swiftlet (statusCode, statusMessage) = http404Errorprint("Код стану дорівнює \(statusCode)")// Надрукує "Код стану дорівнює 404"print("Повідомлення статусу є \(statusMessage)")// Надрукує "Повідомлення статусу є Не знайдено"
```

Якщо потрібно тільки деякі із значень кортежу, можна проігнорувати частини кортежу за допомогою символу підкреслення (`_`) під час декомпозиції кортежу: ```swiftlet (justTheStatusCode, _) = http404Errorprint("Код статусу дорівнює \(justTheStatusCode)")// Надрукує "Код статусу дорівнює 404"
```


Іншим способом доступу до окремих елементів кортежу є числові індекси, які починаються з нульового: 
```swiftprint("Код статусу дорівнює \(http404Error.0)")// Надрукує "Код статусу дорівнює 404"print("Повідомлення статусу є \(http404Error.1)")// Надрукує "Повідомлення статусу є Не знайдено"
```

Також можна іменувати окремі елементи в кортежі під час його оголошення:

```swiftlet http200Status = (statusCode: 200, description: "OK")// Якщо елементи кортежу іменовані,
// можна користуватись їх іменами для доступу до їх значень:
print("Код статусу дорівнює \(http200Status.statusCode)")// Надрукує "Код статусу дорівнює 200"print("Повідомлення статусу є \(http200Status.description)")// Надрукує "Повідомлення статусу є OK"
```

Зокрема, кортежі зручні як значення, що повертають функції. Функція, що намагається отримати веб-сторінку, може повертати кожтеж типу `(Int, String)`, щоб описати успіх чи невдачу при завантаженні сторінки. Повертаючи кортеж з двома окремими значеннями різних типів, функція надає більш корисну інформацію про свій результат, ніж якби вона повертала лише одне значення, чи кілька значень одного типу. З більш детальною інформацією можна ознайомитись у розділі [Функції, що повертають кілька значень](5_functions.md#функції,-що-повертають-кілька-значень)

> **Примітка**
> 
> Кортежі зручно вживати для тимчасових груп пов'язаних значень. Вони не підходять для створення складних структур даних. Якщо структура даних може жити поза тимчасовим контекстом, слід можелювати її за допомогою класу чи структури, а не кортежу. Більш детальну інформацію можна знайти у розділі [Класи і структури](1_language_guide/8_classes_and_structures.md).


### Optionals
You use *optionals* in situations where a value may be absent. An optional represents two possibilities: Either there *is* a value, and you can unwrap the optional to access that value, or there *isn’t* a value at all.> Note
> > The concept of optionals doesn’t exist in C or Objective-C. The nearest thing in Objective-C is the ability to return `nil` from a method that would otherwise return an object, with `nil` meaning “the absence of a valid object.” However, this only works for objects—it doesn’t work for structures, basic C types, or enumeration values. For these types, Objective-C methods typically return a special value (such as `NSNotFound`) to indicate the absence of a value. This approach assumes that the method’s caller knows there is a special value to test against and remembers to check for it. Swift’s optionals let you indicate the absence of a value for *any type at all*, without the need for special constants.
Here’s an example of how optionals can be used to cope with the absence of a value. Swift’s `Int` type has an initializer which tries to convert a `String` value into an `Int` value. However, not every string can be converted into an integer. The string `"123"` can be converted into the numeric value `123`, but the string `"hello, world"` does not have an obvious numeric value to convert to.
The example below uses the initializer to try to convert a `String` into an `Int`:

```swiftlet possibleNumber = "123"let convertedNumber = Int(possibleNumber)// convertedNumber is inferred to be of type "Int?", or "optional Int"
```
Because the initializer might fail, it returns an optional `Int`, rather than an `Int`. An optional `Int` is written as `Int?`, not `Int`. The question mark indicates that the value it contains is optional, meaning that it might contain *some* `Int` value, or it might contain *no value at all*. (It can’t contain anything else, such as a `Bool` value or a `String` value. It’s either an `Int`, or it’s nothing at all.)#### nilYou set an optional variable to a valueless state by assigning it the special value `nil`:

```swiftvar serverResponseCode: Int? = 404// serverResponseCode contains an actual Int value of 404serverResponseCode = nil// serverResponseCode now contains no value
```
> **Note**
> > `nil` cannot be used with nonoptional constants and variables. If a constant or variable in your code needs to work with the absence of a value under certain conditions, always declare it as an optional value of the appropriate type.
If you define an optional variable without providing a default value, the variable is automatically set to `nil` for you:

```swiftvar surveyAnswer: String?// surveyAnswer is automatically set to nil
```
> **Note**> 
> Swift’s `nil` is not the same as `nil` in Objective-C. In Objective-C, `nil` is a pointer to a nonexistent object. In Swift, `nil` is not a pointer—it is the absence of a value of a certain type. Optionals of *any* type can be set to `nil`, not just object types.
#### If Statements and Forced Unwrapping
You can use an `if` statement to find out whether an optional contains a value by comparing the optional against nil. You perform this comparison with the “equal to” operator (`==`) or the “not equal to” operator (`!=`).
If an optional has a value, it is considered to be “not equal to” `nil`:

```swiftif convertedNumber != nil {    print("convertedNumber contains some integer value.")}// Prints "convertedNumber contains some integer value."
```
Once you’re sure that the optional *does* contain a value, you can access its underlying value by adding an exclamation mark (`!`) to the end of the optional’s name. The exclamation mark effectively says, “I know that this optional definitely has a value; please use it.” This is known as *forced unwrapping* of the optional’s value:

```swiftif convertedNumber != nil {    print("convertedNumber has an integer value of \(convertedNumber!).")}// Prints "convertedNumber has an integer value of 123."
```
For more on the `if` statement, see [Control Flow](4_control_flow.md).
> **Note**
> 
> Trying to use `!` to access a nonexistent optional value triggers a runtime error. Always make sure that an optional contains a non-nil value before using ! to force-unwrap its value.

#### Optional Binding
You use *optional binding* to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable. Optional binding can be used with `if` and `while` statements to check for a value inside an optional, and to extract that value into a constant or variable, as part of a single action. if and while statements are described in more detail in [Control Flow](4_control_flow.md).Write an optional binding for an `if` statement as follows:

```swiftif let <constantName> = <someOptional> {    <statements>}
```
You can rewrite the `possibleNumber` example from the [Optionals](#optionals) section to use optional binding rather than forced unwrapping:

```swiftif let actualNumber = Int(possibleNumber) {    print("\"\(possibleNumber)\" has an integer value of \(actualNumber)")} else {    print("\"\(possibleNumber)\" could not be converted to an integer")}// Prints ""123" has an integer value of 123"
```
This code can be read as:“If the optional `Int` returned by `Int(possibleNumber)` contains a value, set a new constant called actualNumber to the value contained in the optional.”
If the conversion is successful, the `actualNumber` constant becomes available for use within the first branch of the if statement. It has already been initialized with the value contained *within* the optional, and so there is no need to use the `!` suffix to access its value. In this example, `actualNumber` is simply used to print the result of the conversion.
You can use both constants and variables with optional binding. If you wanted to manipulate the value of `actualNumber` within the first branch of the `if` statement, you could write `if var actualNumber` instead, and the value contained within the optional would be made available as a variable rather than a constant.
You can include as many optional bindings and Boolean conditions in a single `if` statement as you need to, separated by commas. If any of the values in the optional bindings are nil or any Boolean condition evaluates to `false`, the whole `if` statement’s condition is considered to be `false`. The following `if` statements are equivalent:
```swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {    print("\(firstNumber) < \(secondNumber) < 100")}// Prints "4 < 42 < 100" if let firstNumber = Int("4") {    if let secondNumber = Int("42") {        if firstNumber < secondNumber && secondNumber < 100 {            print("\(firstNumber) < \(secondNumber) < 100")        }    }}// Prints "4 < 42 < 100"
```
> **Note**
> 
> Constants and variables created with optional binding in an `if` statement are available only within the body of the `if` statement. In contrast, the constants and variables created with a `guard` statement are available in the lines of code that follow the `guard` statement, as described in [Early Exit](4_control_flow.md#early-exit).#### Implicitly Unwrapped OptionalsAs described above, optionals indicate that a constant or variable is allowed to have “no value”. Optionals can be checked with an `if` statement to see if a value exists, and can be conditionally unwrapped with optional binding to access the optional’s value if it does exist.
Sometimes it is clear from a program’s structure that an optional will *always* have a value, after that value is first set. In these cases, it is useful to remove the need to check and unwrap the optional’s value every time it is accessed, because it can be safely assumed to have a value all of the time.
These kinds of optionals are defined as *implicitly unwrapped optionals*. You write an implicitly unwrapped optional by placing an exclamation mark (`String!`) rather than a question mark (`String?`) after the type that you want to make optional.
Implicitly unwrapped optionals are useful when an optional’s value is confirmed to exist immediately after the optional is first defined and can definitely be assumed to exist at every point thereafter. The primary use of implicitly unwrapped optionals in Swift is during class initialization, as described in [Unowned References and Implicitly Unwrapped Optional Properties](15_automatic_reference_counting.md#unowned-references-and-implicitly-unwrapped-optional-properties).
An implicitly unwrapped optional is a normal optional behind the scenes, but can also be used like a nonoptional value, without the need to unwrap the optional value each time it is accessed. The following example shows the difference in behavior between an optional string and an implicitly unwrapped optional string when accessing their wrapped value as an explicit `String`:

```swiftlet possibleString: String? = "An optional string."let forcedString: String = possibleString! // requires an exclamation mark let assumedString: String! = "An implicitly unwrapped optional string."let implicitString: String = assumedString // no need for an exclamation mark
```
You can think of an implicitly unwrapped optional as giving permission for the optional to be unwrapped automatically whenever it is used. Rather than placing an exclamation mark after the optional’s name each time you use it, you place an exclamation mark after the optional’s type when you declare it.
> **Note**> 
> If an implicitly unwrapped optional is `nil` and you try to access its wrapped value, you’ll trigger a runtime error. The result is exactly the same as if you place an exclamation mark after a normal optional that does not contain a value.
You can still treat an implicitly unwrapped optional like a normal optional, to check if it contains a value:

```swiftif assumedString != nil {    print(assumedString)}// Prints "An implicitly unwrapped optional string."
```
You can also use an implicitly unwrapped optional with optional binding, to check and unwrap its value in a single statement:

```swiftif let definiteString = assumedString {    print(definiteString)}// Prints "An implicitly unwrapped optional string."
```
> **Note**
> > Do not use an implicitly unwrapped optional when there is a possibility of a variable becoming `nil` at a later point. Always use a normal optional type if you need to check for a `nil` value during the lifetime of a variable.
### Error Handling
You use *error handling* to respond to error conditions your program may encounter during execution.
In contrast to optionals, which can use the presence or absence of a value to communicate success or failure of a function, error handling allows you to determine the underlying cause of failure, and, if necessary, propagate the error to another part of your program.
When a function encounters an error condition, it *throws* an error. That function’s caller can then *catch* the error and respond appropriately.

```swiftfunc canThrowAnError() throws {    // this function may or may not throw an error}
```
A function indicates that it can throw an error by including the `throws` keyword in its declaration. When you call a function that can throw an error, you prepend the `try` keyword to the expression.
Swift automatically propagates errors out of their current scope until they are handled by a catch clause.

```swiftdo {    try canThrowAnError()    // no error was thrown} catch {    // an error was thrown}
```
A `do` statement creates a new containing scope, which allows errors to be propagated to one or more `catch` clauses.
Here’s an example of how error handling can be used to respond to different error conditions:

```swiftfunc makeASandwich() throws {    // ...} do {    try makeASandwich()    eatASandwich()} catch SandwichError.outOfCleanDishes {    washDishes()} catch SandwichError.missingIngredients(let ingredients) {    buyGroceries(ingredients)}
```
In this example, the `makeASandwich()` function will throw an error if no clean dishes are available or if any ingredients are missing. Because `makeASandwich()` can throw an error, the function call is wrapped in a `try` expression. By wrapping the function call in a `do` statement, any errors that are thrown will be propagated to the provided `catch` clauses.
If no error is thrown, the `eatASandwich()` function is called. If an error is thrown and it matches the `SandwichError.outOfCleanDishes` case, then the `washDishes()` function will be called. If an error is thrown and it matches the `SandwichError.missingIngredients` case, then the `buyGroceries(_:)` function is called with the associated `[String]` value captured by the `catch` pattern.Throwing, catching, and propagating errors is covered in greater detail in [Error Handling](17_error_handling.md).
### Assertions
In some cases, it is simply not possible for your code to continue execution if a particular condition is not satisfied. In these situations, you can trigger an *assertion* in your code to end code execution and to provide an opportunity to debug the cause of the absent or invalid value.
#### Debugging with Assertions
An assertion is a runtime check that a Boolean condition definitely evaluates to true. Literally put, an assertion “asserts” that a condition is `true`. You use an assertion to make sure that an essential condition is satisfied before executing any further code. If the condition evaluates to `true`, code execution continues as usual; if the condition evaluates to `false`, code execution ends, and your app is terminated.
If your code triggers an assertion while running in a debug environment, such as when you build and run an app in Xcode, you can see exactly where the invalid state occurred and query the state of your app at the time that the assertion was triggered. An assertion also lets you provide a suitable debug message as to the nature of the assert.
You write an assertion by calling the Swift standard library global `assert(_:_:file:line:)` function. You pass this function an expression that evaluates to `true` or `false` and a message that should be displayed if the result of the condition is `false`:

```swiftlet age = -3assert(age >= 0, "A person's age cannot be less than zero")// this causes the assertion to trigger, because age is not >= 0
```
In this example, code execution will continue only if `age >= 0` evaluates to `true`, that is, if the value of age is non-negative. If the value of `age` is negative, as in the code above, then `age >= 0` evaluates to false, and the assertion is triggered, terminating the application.
The assertion message can be omitted if desired, as in the following example:

```swiftassert(age >= 0)
```
> **Note**
> 
> Assertions are disabled when your code is compiled with optimizations, such as when building with an app target’s default Release configuration in Xcode.#### When to Use Assertions
Use an assertion whenever a condition has the potential to be false, but must *definitely* be true in order for your code to continue execution. Suitable scenarios for an assertion check include:

 + An integer subscript index is passed to a custom subscript implementation, but the subscript index value could be too low or too high.
 + A value is passed to a function, but an invalid value means that the function cannot fulfill its task.
 + An optional value is currently nil, but a non-nil value is essential for subsequent code to execute successfully.
  See also [Subscripts](11_subscripts.md) and [Functions](5_functions.md).

> **Note**
> > Assertions cause your app to terminate and are not a substitute for designing your code in such a way that invalid conditions are unlikely to arise. Nonetheless, in situations where invalid conditions are possible, an assertion is an effective way to ensure that such conditions are highlighted and noticed during development, before your app is published.
