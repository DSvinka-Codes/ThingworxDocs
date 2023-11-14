---
description: Создание Mashup и его дальнейшее редактирование
---

# Mashup

## Создание Mashup

Называемый также веб-интерфейсом, по сути это то, через что мы можем управлять роботом и смотреть от него данными. Грубо говоря в них мы делаем пульты управления.

{% hint style="info" %}
Например у нас есть сотрудник - Инженер. Он занимается обслуживанием роботов. Ему нужно видеть температуру моторов, углы поворотов, координаты, показывать индикторы что что-то не так, и ему нужно иметь кнопку для остановки процессов в экстренном случае.

Всё это делается через Mashup.
{% endhint %}

Когда вы создаете Mashup **(о том как создавать объекты, описано** [**здесь**](sozdanie-obektov.md)**)** у вас появляется диалоговое окно, где просят выбрать тип Mashup'а. Для простоты работы мы используем `Static (Legacy)`

<figure><img src="broken-reference" alt="" width="359"><figcaption></figcaption></figure>

Ставим любое удобное название, если надо описание, логотип. Выбираем проект, к которому принадлежит Mashup и всё, Mashup готов.

Для вёрстки Mashup (добавление и редактирование элементов) нужно перейти во вкладку Design

<img src="broken-reference" alt="" data-size="original">

Также если мы хотим посмотреть что у нас получается в итоге, можно нажать на кнопку ![](broken-reference) она находится справа от названия вашего Mashup'a

## Подключение сервисов вещей к Mashup

Для того чтобы получать/устанавливать Properties вещей используются стандартные сервисы `GetProperties` и `SetProperties`.

Также вы можете подключать и вызывать свои сервисы.

Чтобы подключить и использовать встроенный или свой сервис используется вкладка Data в правой части экрана. Нажмите кнопку с иконкой плюсика чтобы добавить сервис.

<figure><img src="../.gitbook/assets/image (14).png" alt="" width="251"><figcaption></figcaption></figure>

У нас появится диалоговое окно. В поле `Entity Type` указываем `Things`\
В поле Entity указываем вашу вещь и выбераем её, в моем случае это `Robot21`.

<figure><img src="../.gitbook/assets/image (15).png" alt="" width="290"><figcaption></figcaption></figure>

Затем вы можете подключить `GetProperties` и `SetProperties`. \
Первый отвечает за получение Property из вещи, например для отображения значения в [LED Display](layout-mashup.md#led-display). \
Второй отвечает за запись данных в Property вещи, например для записи значения полученного через [Numeric Entry](layout-mashup.md#numeric-entity).

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Не забудьте при добавлении `GetProperties` поставить галочку под пунктом<img src="../.gitbook/assets/image (36).png" alt="" data-size="line"> чтобы значения Property загружались при открытии страницы Mashup'а.

**Возьмите за правило. На всем сервисах которые начинаются с `Get` мы ставим галочку `Execute on Load`**
{% endhint %}

В этом же списке также можно смотреть и добавлять сервисы созданные вами.

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Если вы добавите новый Property и хотите чтобы он отобразился в `GetProperties`/`SetProperties` то нажмите кнопку ![](<../.gitbook/assets/image (26).png>) для обновления списков. Эта кнопка справа от кнопки плюсика (та что подключает сервисы в Mashup)
{% endhint %}

## Подключение сервисов к виджетам Mashup'а

### Получение данных из Properties

Для того чтобы получать данные из Properties используется сервис `GetProperties`, вы можете раскрыть его и получить доступ ко всем Property на выбранной вещи.&#x20;

Чтобы элемент Mashup'a имел доступ к данным из Property, возьмите Property мышкой и перенесите на нужный элемент, и в сплывающем меню выберите `Data`.

<figure><img src="../.gitbook/assets/image (27).png" alt="" width="239"><figcaption></figcaption></figure>

Таким образом, например [LED Display](layout-mashup.md#led-display) будет отображать данные из этого Property, а в [Shape ](layout-mashup.md#shape)будет работать State Formatter.

Помните что данные в GetProperties сами не обновляются. Для обновления данных нужно просто вызвать сервис GetProperties. Подробнее об этом в [#vyzov-servisov](layout-mashup.md#vyzov-servisov "mention")

### Запись данных в Properties

Для записи данных в Properties можно использовать как ваши сервисы (вызывать сервисы с Input параметрами), так и встроенный SetProperties.

### Вызов сервисов

Существует 3 основных способа вызывать сервисы: Через кнопку/shape, Через `AutoRefresh`, Через `ServiceInvokeCompleted`.

#### Через кнопку/shape

Сначала нужно направить мышку на Кнопку/Shape в левый верхний угол, у вас откроется меню. Далее выполняет пункты с картинки:&#x20;

<figure><img src="../.gitbook/assets/image (29).png" alt="" width="439"><figcaption></figcaption></figure>

Таким образом мы привязаываем кнопку так, чтобы при её нажатии вызывался `Move_Service`. Раскрывать сервис не требуется, просто зажмите мышку на `Clicked` и отпустите мышку на названии нужного сервиса.

#### Через AutoRefresh

## Виджеты Mashup'а

В Thingworx очень много различных виджетов, от квадрата до целого блога .-.\
По этому мы затронем только основные виджеты которые используются повседневно.

Виджеты можно добавлять на Mashup с помощью левой менюшки

<figure><img src="../.gitbook/assets/image (30).png" alt="" width="314"><figcaption><p>Просто перенесите мышкой элемент на Mashup и он появится</p></figcaption></figure>

### Кнопка

![](broken-reference) - Обыкновенная кнопка. Кнопки могут запускать сервисы, для этого используется ивент Clicked. Для того чтобы получить к нему доступ, нажмите на стрелочку в верхнем левом углу кнопки (там, куда направлена красная стрелка на скриншоте ниже) и перетащите мышкой Clicked на сервис который хотите вызвать.&#x20;

<figure><img src="broken-reference" alt=""><figcaption><p>Меню где можно взять мышкой ивент Clicked <br>и перетащить на любой сервис для его запуска при нажатии</p></figcaption></figure>

Во вкладке Properties можно менять текст кнопки (с `Button` на что-то другое) и расположение текста

&#x20;

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

### LED Display

<img src="../.gitbook/assets/image (33).png" alt="" data-size="line"> - Отображает цифры, например значение Property.&#x20;

### Shape



### Numeric Entity

