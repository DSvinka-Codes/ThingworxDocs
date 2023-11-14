# Полезные примеры

## Мигающий светофор

В [contest.md](../contest.md "mention") описаны задания на мигающий светофор. Этот случай мы и разберём.

Для начала вам потребуется в светофоре [создать новый сервис](../thingworx-web/veshi.md#sozdanie-servisa) и сделать его Async (асинхронным). &#x20;

<div align="center">

<figure><img src="../.gitbook/assets/image (40).png" alt="" width="232"><figcaption></figcaption></figure>

</div>

Таким образом при вызове этого сервиса из другого сервиса, этот сервис будет выполнятся в  фоне. То есть если в сервисе InOutService мы вызовем сервис BlinkLightService, то InOutService не будет ждать пока BlinkLightService завершит работу.\
Это позволит светофору мигать даже когда робот выполняет какой то код.

Для начала давайте определим какие Property мы должны создать.

* `blinkAlreadyRun` `[Boolean]` - Запущен ли сервис мигания. Смотрите комментарий к 8 строке кода ниже.
* `blinkColor` `[Integer]` - Число обозначающее цвет, который должен мигать. 0 - прекращает мигание. 1 - зеленый. 2 - жёлтый. 3 - красный. 4 - синий.
* `lightGreen`, `lightYellow`, `lightRed`, `lightBlue` `[Boolean]` -  обозначают цвета светофора которые передаются в InOutService. То есть если включить любую из Property то на светофоре загорится цвет, соответствующий названию Property.

Далее напишем код который будет выполнять мигание.

{% code lineNumbers="true" %}
```javascript
// Объявляем цвета
const Colors = { NONE: 0, GREEN: 1, YELLOW: 2, RED: 3, BLUE: 4 };

// Требуется чтобы после завершения сервиса, мигающая лампочка выключалась а не оставалась включенной.
let currentBlinkLight;
 
// Защита от повторной активации сервиса.
// Дело в том, что сейчас сервис написан так, что он поддерживает только мигание 
// одного цвета за раз. Если этот сервис запустить ещё раз, то мегание будет
// сломано.
if (!me.blinkAlreadyRun)
{
  me.blinkAlreadyRun = true;

  while (me.blinkColor != 0) {
    currentBlinkLight = me.blinkColor;

    // Меняем состояние определенного цвета светофора на противоположное.
    // Таким образом происходит мигание, пока blinkColor содержит номер цвета, 
    // мигание будет продолжатся. В ином случае мигание прекратится.
    switch (me.blinkColor) {
      case 1:
        me.lightGreen = !me.lightGreen;
        break;
      case 2:
        me.lightYellow = !me.lightYellow;
        break;
      case 3:
        me.lightRed = !me.lightRed;
        break;
      case 4:
        me.lightBlue = !me.lightBlue;
        break;
    }
  
    // Пауза в 1 секунду
    pause(1 * 2000);  
  }
  
  // Когда цикл завершен, не забывает отметить что мигание выключено 
  me.blinkAlreadyRun = false;

  // И не забываем выключить лампочку (бывает что цикл останавливается когда лампа включена)
  switch (currentBlinkLight) {
      case 1:
        me.lightGreen = false;
        break;
      case 2:
        me.lightYellow = false;
        break;
      case 3:
        me.lightRed = false;
        break;
      case 4:
        me.lightBlue = false;
        break;
    }
}
```
{% endcode %}

**На самом деле нечего сложного тут нет.**&#x20;

Только можно отметить что мы используем `switch` вместо `if else` так как в данном случае `switch` тут будет уместнее, удобнее, ну и компактнее :D&#x20;

Остается только выбрать цвет и вызвать сервис (например через мешап и переключатели)
