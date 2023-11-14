---
description: Роботы, Светофоры, Пульты, Сканеры
---

# Вещи

## Создание Вещи

Давайте нажмем на кнопку `Thing` **(о том где находится это кнопка, описано** [**здесь**](sozdanie-obektov.md)**)**, у нас появится окно создания проекта, здесь вы можете указать объязательно название, и по желанию логотип, описание, документацию.

Вещи это непосредственно устройства которыми вы управляете, робот, светофор, панель управления, сканер кода.

При создании вещей нужно быть **КРАЙНЕ** внимательным, и не торопится.&#x20;

Когда пишите **название вещи** <mark style="color:red;">**ОШИБКИ НЕДОПУСТИМЫ.**</mark>\
Название вещи СТРОГО указываем также как в [parametry-veshei](../code/parametry-veshei/ "mention"), подставляя свои номера команд. \
<mark style="color:red;">**Потом название уже сменить нельзя будет.**</mark> И вам придется или пересоздавать вещь, или преподавателю менять настройки Thingworx.

Здесь по мимо стандартных полей есть ещё поле <mark style="color:yellow;">**Base Thing Template**</mark>, на всех вещах в этом поле выбераем **GenericThing**

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

На этом создание вещи закончено.

## Создание Property

На странице [#rabota-s-properties](../code/property-i-parametry.md#rabota-s-properties "mention") мы обсуждали как работать с Properties из кода, самое время их начать создавать. Для создания нам нужно зайти в нашу вещь, во вкладку ![](<../.gitbook/assets/image (17).png>) там есть кнопка ![](<../.gitbook/assets/image (18).png>) по нажатии на которую, справа появится окно создания Property.

* Для начала укажем название. \
  Во первых название не должно пересекаться с [параметрами мониторинга и управления вещей](../code/parametry-veshei/). \
  Во вторых название должно начинатся с буквы, желательно английского языка.\
  Иначе код может просто не работать.
* Затем можно указать описание по желанию.
* Дальше указываем тип (`Base Type`), я например выберу Integer (число)
* В случае с Integer мы можем указать минимальное (`Min Value`) и максимальное (`Max Value`) значение. Укажем для примера что число должно быть от 2 до 10.
* Далее в поле `Has Default Value` мы можем указать что Property имеет значение по умолчанию, я поставлю значение 5.
* Дальше у нас есть настройка `Persistent`, весьма специфичный параметр. Если его включить то Propery не будет сбрасываться при перезагрузки вещи или системы.
* Настройка `Read Only` позволяет запретить записывать данные в Property, полезно когда нужно создать переменную с значением которое не следует изменять.

<figure><img src="../.gitbook/assets/image (19).png" alt="" width="369"><figcaption></figcaption></figure>

После произведения настройки, у нас есть 3 кнопки в верхнем правом углу, галка с плюсом, галка, и знак запрета. Галка с плюсом сохраняет изменения и позволяет сразу же создать ещё один Property. Обычная галка тоже сохраняет изменения, но закрывает меню редактирование Property. А знак запрета просто отменяет изменения.

## Создание Сервиса

Для этого перейдём во вкладку ![](<../.gitbook/assets/image (21).png>), там нажимаем на кнопку ![](<../.gitbook/assets/image (22).png>) и мы попадаем в наш сервис.

Слева указываем название сервиса, по желанию описание.

{% hint style="info" %}
Вообще для редактирования кода в сервисах я могу посоветовать поставить [плагин](https://github.com/ptc-iot-sharing/MonacoEditorTWX), с ним гораздо прияттнее писать код.
{% endhint %}

{% hint style="danger" %}
Если вы хотите чтобы сервис мог возвращать/принимать значения от/к вещи, то он должен иметь название <mark style="color:yellow;">**InOutService**</mark>

**Обычные сервисы умеют только работать с Properties и** [**другими сервисами**](../code/utility.md#obrashenie-veshei-k-drugim-vesham)**.**

Затем необходимо в `Input` добавить названия переменных мониторинга которые мы хотим использовать, например как на скрине ниже

![](<../.gitbook/assets/image (24).png>)

А если вы хотите возвращать значения обратно в робота, то необходимо в `Output` указать `JSON`.

![](<../.gitbook/assets/image (25).png>)
{% endhint %}

В сервисах мы можем писать код на Javascript.

В [Broken link](broken-reference "mention") и [Broken link](broken-reference "mention") подробно описывается написание кода.