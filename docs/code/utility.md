---
description: Различные методы и фишки JS, полезные при работе с Thingworx
---

# Утилиты

## Обращение вещей к другим вещам

```js
Things["TrafficLights51"].example1 = true
// где "example1" это Properties переменная булевого типа вещи "TrafficLight51".
// (тип и название меременной может быть любым)
```

```js
Things["TrafficLights51"].ExampleService()
// где "ExampleService" это сервис который я создал в светофоре.
```

Также сервисы могут [возвращать и принимать значения](../thingworx-web/veshi.md#sozdanie-servisa).

```javascript
me.moveSuccess = Things["Robot21"].MoveService({x: 5, y: 10});
```

В этом примере мы в роботе создаем сервис `MoveService`, который двигает робота на указанную позицию. В настройках сервиса, в `Input` указаны переменные `x`, `y`, с типом `Integer`. А в `Output` указан тип `Boolean`. &#x20;

## Работа с разными типами

Более подробно о переводе и работе с типами вы можете почитать в категории [data-types](../javascript/data-types/ "mention")

<pre class="language-js"><code class="lang-js"><strong>/* Перевод строки в число */
</strong><strong>me.example1 = parseInt(m1)
</strong>// Где в "me.example1" записывается получившееся число,
// а "m1" это строка которую нужно превратить в число.

/* Перевод строки в число, второй вариант */
me.example1 = +m1
// Где в "me.example1" записывается получившееся число,
// а "m1" это строка которую нужно превратить в число.

/* Перевод булевого значения в число */
result = {V: +me.Vacuum}
// Где в "V" записывается получившееся число,
// а "me.Vacuum" это булевое значение.

/* Перевод числа в булевое значение */
me.exampleBool = Boolean(me.example1)
// Где в "me.exampleBool" записывается получившееся булевое значение,
// а "me.example1" это число которое нужно перевести. (Значение должно быть или 0 или 1)
</code></pre>

## Пауза в коде

Thingworx позволяет ставить паузу в работе кода. При этом робот продолжает движение.&#x20;

```javascript
/* Пауза в коде */
pause(2000)
// Где 2000 это число миллисекунд.
// При паузе код останавливается, но робот продолжает движения. 
// Когда пройдет 2 секунды, код дальше продолжит работу 
```

{% hint style="danger" %}
Внутри [циклов ](../javascript/cikly.md)функция`pause()` не работает! НО работает только циклах [`while`](../javascript/cikly.md#cikl-while)`!!`!
{% endhint %}

