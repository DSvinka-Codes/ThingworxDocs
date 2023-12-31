---
description: >-
  Как получить данные из вещей, Как отправить данные в вещи, Как работать с
  Properties
---

# Property и Параметры

Названия переменных описаны в категории [parametry-veshei](parametry-veshei/ "mention").&#x20;

* Переменные которые мы получаем от вещей мы будем называть **Параметрами Мониторинга.**
* А переменные которые мы отправляем вещам будем называть **Параметрами Управления.**
* Пользовательские переменные, которые мы можем создать в вещи, мы будем называть **Properties** или **Property**

## Работа с Properties

Сначала в вещи нужно создать эти самые Properties.

Это делается в вещи, во вкладке Properties, [#sozdanie-property](../thingworx-web/veshi.md#sozdanie-property "mention")

Допустим мы создали Property `motorRaw` с типом Integer. В него мы можем записать сырое значения с робота.

К Properties можно получить доступ через me - `me.motorRaw`

{% hint style="info" %}
Далее мы разберём запись и получение данных из Property.

В большей части данной шпаргалки, в примерах, используется запись и чтение именно в Property, хотя иногда будут использоваться [переменные](../javascript/peremennye.md).
{% endhint %}

## Получение данных из вещей

**Для начала запомните важную вещь:** что получение данных из вещи работает только в сервисе `InOutService.`

Также для получения данных нужно в параметрах сервиса в `Input` добавить нужные Параметры Мониторинга вашей вещи, например `m1`, `m2`, `t1`, `t2` и т.п

Далее можно писать код, например запишем параметр мониторинга `m1` в Property `motorRaw`

```javascript
// Например m1 равен 5

me.motorRaw = m1;  // motorRaw теперь содержит цифру 5
me.motorRaw = m1 + 10;  // Прибавляем к m1 цифру 5 и записываем результат
me.motorRaw = me.motorRaw + m1; // Прибавляем к старому значению motorRaw, новое из m1 
me.motorRaw += m1;  // Тоже самое что пример выше
```

Стоит отметить что конструкция += работает и с другими математическими операторами: `+=`, `-=`, `/=`, `*=` это позволяет сократить код и сделать его более приятным для чтения.

Также бывает что кто-то путается и думает что когда мы пишем конструкцию подобную этой: `m1 + 10`, то m1 изменяется, но это не так. Чтобы она изменилась нужно написать `m1 += 10`

## Отправка данных в вещи

Для того чтобы отправить данные в вещь нужно знать что отправка данных в вещьи работает только в сервисе `InOutService` в котором `Output` установлен в `JSON`.

Для отправки данных в вещи используется конструкция `result = {}`.

{% hint style="info" %}
Подробнее об объектах (фигурные скобки) можно узнать в [objects.md](../javascript/data-types/objects.md "mention")
{% endhint %}

Опять же в пример возьмём робота, у него есть Параметр Управления `X` который принимает число. Чтобы изменить этот параметр нам нужно в `result` его добавить в качестве ключа, и добавить некое значение.

```javascript
result = {
  X: 90
}
```

Или

```javascript
result = {
  "X": 90 
}
```

Также можно вместо конкретного значения, подставить Property

```javascript
result = {
  X: me.exampleX
}
```

Всего можно передать не ограниченное количество параметров, просто разделяйте их через запятую и всё будет хорошо :)

```javascript
result = {
  X: me.exampleX,
  Y: me.exampleY
}
```
