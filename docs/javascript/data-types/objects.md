---
description: То что пишется в фигурных скобках, их ещё словарём называют
cover: broken-reference
coverY: 9
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Объекты (Json)

## Создание объектов

Вообще в Javascript есть два способа создания объектов, через конструктор (`let x = new Object()`) и через литерал (`let x = {}`).

```javascript
result = {     // объект
  name: "John",  // под ключом "name" хранится значение "John"
  "age": 30        // под ключом "age" хранится значение 30
};
```

Как можно увидеть на этом примере мы возвращаем результат в переменную result, это штука только для Thingworx, в "чистом" Javascript используется конструкция:

```javascript
return {
  name: "John",
  "age": 30
};
```

Но подробнее о конструкции return мы будем обсуждать в главе [functions.md](../functions.md "mention").

Также в этих примерах можно увидеть что ключи (то что слева от знака `:`) мы можем писать как с кавычками так и без них.

## Получение данных из объектов

Поля это как [переменные ](../peremennye.md)только внутри [объекта](objects.md). Для примера мы можем взять `me.exampleField`. В данном случае `me` это объект, а `exampleField` это поле.&#x20;

Давайте создадим объект и попробуем из него взять какую ту информацию. В этом примере мы будем использовать [переменные](../peremennye.md).

```javascript
let abc = {
    a: 1,
    b: 2,
    c: 3
};

me.exampleNumber = abc.a;  // Запишется цифра 1
me.exampleNumber = abc.b;  // Запишется цифра 2
me.exampleNumber = abc.c;  // Запишется цифра 3

me.exampleNumber = abc["a"];  // Так тоже можно, запишется цифра 1
```

Как вы могли увидеть, можно использовать 2 способа получения данных, через точку и через квадратные скобки и строку.

## Перевод объектов в строку (`JSON.stringify`)

JavaScript предоставляет методы:

* `JSON.stringify` для преобразования объектов в JSON.
* `JSON.parse` для преобразования JSON обратно в объект.

Например, здесь мы преобразуем через `JSON.stringify` данные робота:

```javascript
let robot = {
  x: 40,
  y: 30,
  vacuum: false,
  moveLog: ['x30y60', 'x40y40', 'x50y-50'],
};

me.exampleString = JSON.stringify(student);

/* запишет объект в формате JSON:
{
  "x": 40,
  "y": 30,
  "vacuum": false,
  "moveLog": ['x30y60', 'x40y40', 'x50y-50'],
}
*/
```

Метод `JSON.stringify(student)` берёт объект и преобразует его в строку.

## Перевод строки в объект (`JSON.parse`)

Чтобы декодировать JSON-строку, нам нужен другой метод с именем `JSON.parse`.

Например:

```javascript
// строковый массив
let numbers = "[0, 1, 2, 3]";

let numbersArray = JSON.parse(numbers);

me.exampleNumber = numbersArray[1];  // 1
```

Или для вложенных объектов:

```javascript
let robot = '{ "x": 30, "y": 40, "vacuum": false, "moveLog": ["x50y20", "x-30y20", "x10y10"] }';

let robotObject = JSON.parse(robot);

me.exampleNumber = robotObject.moveLog[1]; // "x-30y20"
```

JSON может быть настолько сложным, насколько это необходимо, объекты и массивы могут включать другие объекты и массивы. Но они должны быть в том же JSON-формате.

Вот типичные ошибки в написанном от руки JSON (иногда приходится писать его для отладки):

```javascript
let json = `{
  name: "John",                     // Ошибка: имя свойства без кавычек
  "surname": 'Smith',               // Ошибка: одинарные кавычки в значении (должны быть двойными)
  'isAdmin': false,                 // Ошибка: одинарные кавычки в ключе (должны быть двойными)
  "birthday": new Date(2000, 2, 3), // Ошибка: не допускается конструктор "new", только значения
  "gender": "male"                  // Ошибка: отсутствует запятая после непоследнего свойства
  "friends": [0,1,2,3],             // Ошибка: не должно быть запятой после последнего свойства
}`;
```

Кроме того, JSON не поддерживает комментарии. Добавление комментария в JSON делает его недействительным.
