---
description: Числа, цифры, математика,
---

# Number (Integer)

В переменные типа Number вмещаются числа со значением `2^53 - 1`  это примерно 9 квадриллионов, в отрицательную сторону такое же максимальное значение.

С числами поддерживаются [математические операции](../operatory-matematicheskie.md)

Для того чтобы превратить строку в число можно использовать следующие конструкции

```javascript
me.exampleString = "50";
me.exampleNumber = Number(me.exampleString);
// Результат: 50
me.exampleNumber = parseInt(me.exampleString);
// Результат: 50
me.exampleNumber = Number.parseInt(me.exampleString);
// Результат: 50

me.exampleString = "Не Число";
me.exampleNumber = Number(me.exampleString);
// Результат: NaN
// Для других конструкций результат будет тот же.
```

Правила численного преобразования:

<table><thead><tr><th width="182.5">Значение</th><th>Преобразуется в…</th></tr></thead><tbody><tr><td><code>true / false</code></td><td><code>1</code> / <code>0</code></td></tr><tr><td><code>string</code></td><td>Пробельные символы (пробелы, знаки табуляции , знаки новой строки  и т. п.) по краям обрезаются. Далее, если остаётся пустая строка, то получаем <code>0</code>, иначе из непустой строки «считывается» число. При ошибке результат <code>NaN</code>.</td></tr></tbody></table>

Примеры преобразований из таблицы:

```javascript
me.exampleNumber = Number(" 123 "); // 123 
me.exampleNumber = Number("123z"); // NaN (ошибка чтения числа на месте символа "z") 
me.exampleNumber = Number(true); // 1 
me.exampleNumber = Number(false); // 0
```
