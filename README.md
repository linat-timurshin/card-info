# CardInfo.js
CardInfo.js позволяет по номеру карты получить логотип банка и типа, фирменные цвета и прочее. Используйте эти данные, чтобы верстать красивые формы для приёма банковских карт. В базе сейчас 50 самых популярных российских банков, позже будут добавлены банки и для других стран, тогда же будет переведна документация на английский язык.

![](https://habrastorage.org/files/6c2/d82/3ac/6c2d823acd4e433e806f306d52255829.gif)

## Быстрый старт
[Скачайте CardInfo.js](https://github.com/iserdmi/card-info/archive/master.zip), установите через bower `bower install card-info` или npm `npm install card-info`.

Подключите JS файл с плагином к странице:
```html
<script src="/bower_components/card-info/dist/card-info.min.js"></script>
```

Теперь можете использовать класс `CardInfo` в своём коде:
```js
var cardInfo = new CardInfo('4377730000000000');
console.log('Название банка:', cardInfo.bankName); 
// > Название банка: Тинькофф Банк
console.log('Логотип банка:', cardInfo.bankLogo); 
// > Логотип банка: /bower_components/card-info/dist/banks-logos/ru-tinkoff.svg
```

## Конструктор
```
new CardInfo(number)
new CardInfo(number, options)
```

* **`number`** номер карты, число или строка, в строке допустимы пробелы.
* **`options`** объект с настройками.


## Экземпляр
Если по первым 6 цифрам в номере карты не удалось определить данные о банке, поля bankAlias, bankName, bankNameEn, bankCountry, bankUrl, bankLogoPng, bankLogoSvg, bankLogo, bankLogoStyle, backgroundColor, backgroundColors, backgroundLightness, textColor, backgroundGradient будут иметь значение по умолчанию.

Если по первым цифрам в номере карты не удалось определить данные о типе, поля brandAlias, brandName, brandLogoPng, brandLogoSvg, brandLogo, codeName, codeLength, numberLengths, numberGaps будут иметь значение по умолчанию.

* **`bankAlias`** по умолчанию `null`  
  Короткое название банка на английском, все буквы маленькие, без пробелов. Если банк не определён, значение `null`.
* **`bankName`** по умолчанию `null`  
  Название банка на языке той страны, в которой работает банк.
* **`bankNameEn`** по умолчанию `null`  
  Название банка на английском.
* **`bankCountry`** по умолчанию `null`  
  Код страны в которой работает этот банк. `'ru'` — Россия.
* **`bankUrl`** по умолчанию `null`  
  Ссылка на сайт банка.
* **`bankLogo`** по умолчанию `null`  
  Путь к логотипу банка. Для каждого банка в папке `dist/banks-logos` есть логотип в формате PNG, для некоторых ещё и в SVG. Имя файла определяется свойством экземпляра `bankAlias`. Путь к файлу определяется свойством настроек `banksLogosPath`. Расширение логотипа определяется свойтсвом настроек `preferredExt`. Пример: для банка «Тинькоф» значение будет `'/bower_components/card-info/dist/banks-logos/ru-tinkoff.svg'`.
* **`bankLogoPng`** по умолчанию `null`  
  Путь к логотипу банка в формате PNG.
* **`bankLogoSvg`** по умолчанию `null`  
  Путь к логотипу банка в формате SVG, если для этого банка существует логотип в формате SVG.
* **`bankLogoStyle`** по умолчанию `null`  
  Если логотип преимущественно чёрный, то `"black"`, если белый, то `"white"`, если цветной, то `"colored"`.
* **`backgroundColor`** по умолчанию `'#eeeeee'`  
  Цвет ассоциирующийся с банком. Если банк не определён, значение будет `'#eeeeee'`.
* **`backgroundColors`** по умолчанию `['#eeeeee', '#dddddd']`  
  Массив цветов ассоциирующихся с банком. Если банк не определён, значение будет `['#eeeeee', '#dddddd']`.
* **`backgroundLightness`** по умолчанию `'light'`  
  Если цвет фона светлый, то значением будет строка `'light'`, иначе `'dark'`.
* **`backgroundGradient`** по умолчанию `linear-gradient(135deg, #eeeeee, #dddddd)`  
  Содержит строку с CSS значением свойства `background`, установив которое, вы получите градиент из цветов указанны в поле `backgroundColors`. Угол можно указать в свойстве настроек `gradientDegrees`.
* **`textColor`** по умолчанию `'#000'`  
  Цвет текста, который хорошо будет виден на фоне указанном в свойстве `backgroundColor`.
* **`brandAlias`** по умолчанию `null`  
  Короткое название типа на английском, все буквы маленькие, без пробелов.
* **`brandName`** по умолчанию `null`  
  Полное название типа.
* **`brandLogo`** по умолчанию `null`  
  Путь к логотипу типа. Для каждого типа в папке `dist/brands-logos` есть логотип в формате PNG и SVG и в трёх стилях: чёрном, белом и цветном. Имя файла определяется свойством экземпляра `brandAlias`. Путь к файлу определяется свойством настроек `brandsLogosPath`. Расширение логотипа определяется свойтсвом настроек `preferredExt`. Стиль логотипа определяется свойтсвом настроек `brandLogoPolicy`. Пример: для типа «Visa» значение будет `'/bower_components/card-info/dist/brands-logos/visa-colored.svg'`.
* **`brandLogoPng`** по умолчанию `null`  
  Путь к логотипу типа в формате PNG.
* **`brandLogoSvg`** по умолчанию `null`  
  Путь к логотипу типа в формате SVG.
* **`codeName`** по умолчанию `null`  
  Название кода на обратной стороне карты (CVC/CID/CVV/CVN).
* **`codeLength`** по умолчанию `null`  
  Ожидаемая длина кода безопасности. Обычно 3, но для карт American Express 4.
* **`numberMask`** по умолчанию `null`  
  Маска для номера карты данного типа. Обычно маска 0000 0000 0000 0000, но некоторые типы карт имеют отличную от 16 символов длину номера карты, и пробелы расставляются в других местах. Например для карт American Express маска будет 0000 000000 00000. Символы в маске могут быть изменены путем изменения настроек `maskDigitSymbol` и `maskDelimiterSymbol`. Используйте свойство `numberMask` для наложения маски на поле ввода номера карты.
* **`numberGaps`** по умолчанию `[4, 8, 12]`  
  Массив с числами, определяющими положение пробелов при создании маски.
* **`numberLengths`** по умолчанию `[16]`  
  Массив с числами, определяющими допустимое количество символов в номере карты.
* **`numberNice`**  
  Номер карты приведённый к красивому виду. Маска определяется свойством `numberMask`. Пример: 4377730000000000 → 4377 7300 0000 0000, 437773 → 4377 73.
* **`number`**  
  Номер карты в виде строки с удалёнными пробелами. Если в переданном номере карты были какие либо символы кроме цифр и пробелов, будет пустой строкой.
* **`numberSource`**  
  Номер карты переданный при создании экземпляра.
* **`options`**  
  Настройки использованные при создании экземпляра.

## Настройки
* **`banksLogosPath`** по умолчанию `'/bower_components/card-info/dist/banks-logos/'`.  
  Путь к файлам с логотипами банков.
* **`brandsLogosPath`** по умолчанию `'/bower_components/card-info/dist/brands-logos/'`.  
  Путь к файлам с логотипами типов.
* **`brandLogoPolicy`** по умолчанию `'auto'`.  
  Эта настройка определяет стиль логотипа типа. Доступные значения: 'black', 'white', 'colored', 'auto', 'mono'.
  * `'colored'`  
    Логотип типа будет цветным
  * `'black'`  
    Логотип типа будет чёрным
  * `'white'`  
    Логотип типа будет белым
  * `'mono'`  
    Логотип типа будет белым, если фон (`backgroundLightness`) тёмный ('`dark'`)
    Логотип типа будет чёрным, если фон (`backgroundLightness`) светлый (`'light'`)
  * `'auto'`  
    Логотип типа будет цветным, если стиль логотипа банка (`bankLogoStyle`) цветной (`'colored'`)
    Логотип типа будет белым, если стиль логотипа банка (`bankLogoStyle`) белый (`'white'`)
    Логотип типа будет чёрным, если стиль логотипа банка (`bankLogoStyle`) чёрный (`'black'`)
    Логотип типа будет цветным, если банк не определён
* **`preferredExt`** по умолчанию `'svg'`.  
  Предпочтительное расширение для логотипов банков и типов. Значением может быть `'png'` или `'svg'`.
* **`maskDigitSymbol`** по умолчанию `'0'`  
  Символ обозначающий цифру в маске номера карты, указанной в свойстве экземпляра `numberMask`.
* **`maskDelimiterSymbol`** по умолчанию `' '`  
  Символ обозначающий разделитель в маске номера карты, указанной в свойстве экземпляра `numberMask`. 
* **`gradientDegrees`** по умолчанию `135`  
  Градус под которым идёт градиент указанный в свойстве экземпляра `backgroundGradient`.

## Статические методы
* **`CardInfo.setDefaultOptions(options)`**  
  Единожды установив настройки по умолчанию они будут применены при каждом создании экземпляра.

## Статические свойства
* **`CardInfo.banks`**  
  Объект с данными по каждому банку. Ключи — короткие название банков (bankAlias).

## Способы подключения
1. Подключить основной файл. В таком случае вы загрузите всю базу данных банков.
```html
<script src="/bower_components/card-info/dist/card-info.min.js"></script>
```

2. Подключить только файл с логикой, без базы данных, а базу данных для вашей страны отдельно. Базы банков отдельно для каждой страны находятся в папке «dist/banks-and-prefixes».
```html
<script src="/bower_components/card-info/dist/card-info.core.min.js"></script>
<script src="/bower_components/card-info/dist/banks-and-prefixes/ru.min.js"></script>
```

3. Подключить в качестве модуля в своём коде
```js
const CardInfo = require('card-info')
// или
import CardInfo from 'card-info'
```

## Нарезка логотипов
Все логотипы банков в исходном размере хрнятся в папке `src/banks-logos`. Если вы устанавливали CardInfo.js чере npm вам будет доступна команда `npm run build-banks-logos`. После её вызова, все логотипы из папки `src/banks-logos` будут преображены в формат PNG, уменьшены до 600 пикселей по ширине и 200 по высоте, скопированы в папку `dist/banks-logos`. Чтобы изменить настройки нарезки логотипов, передайте настройки при вызове команды вот так `npm run build-banks-logos -- -w 1000 -h 300`

* **`-w  | --width`** по умолчанию `600`  
  Ширина в пикселях до которой будет уменьшено/увеличено изображение
* **`-h | --height`** по умолчанию `200`  
  Высота в пикселях до которой будет уменьшено/увеличено изображение
* **`-n | --enlargement`** по умолчанию отключено  
  Если изображение меньше по ширине или высоте, чем переданные в настрйоках значения, то картинка не будет увеличина. Однако, если передать эту опцию, то картинка будет увеличина принудительно.
* **`-e | --embed`** по умолчанию отключено  
  Изображение уменьшается/увеличивается пропорционально своим исходным размером. Так к примеру картинка 600×200, при нарезке с опциями `-w 200 -h 100` станет 200×50. Однако, если передать эту опцию, то картинка станет 200×100, а пустое пространство займёт прозрачная область.

Вся информация выше также распространяется на логотипы типов. Команда: `npm run build-brands-logos`. Исходная папка: `src/brands-logos`. Конечная папка: `dist/brands-logos`. По умолчанию высота 60 пикселей, а ширина не указана.

## Работоспособность
Код проверн и работает во всех браузерах включая Internet Explorer 6. Чтобы прогнать тесты выполните команду `npm test` или откройте в браузере файл `test/browser/main.html`.

## Особая благодарность
Спасибо [BIN Codes](https://www.bincodes.com) за актуальную базу префиксов для всех банков  
Спасибо [Stuart Colville](https://muffinresearch.co.uk/svg-credit-card-icons/) за логотипы типов  
Спасибо [Евгению Катышеву](http://evgenykatyshev.ru/notes/all/mir-logo/) за логотип платёжной системы МИР  

## Нравится плагин?
Можете поблагодарить меня словами или деньгами [на этой странице.](http://srdm.io/спасибо)
