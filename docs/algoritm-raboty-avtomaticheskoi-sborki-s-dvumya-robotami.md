# Алгоритм работы автоматической сборки с двумя роботами

1. Создать DataShape (заголовки таблицы) с полями `x`, `y`, `z`, `v`
2. Создать переменные в первом роботе:&#x20;
   * `line` (по умолчанию: `-1`) данная переменная будет отвечать за номер строки в таблице.&#x20;
   * `pause` булевская переменная, включение/выключение сборки.
   * `light` для переключения цветов на светофоре
3. Создать переменную `line`, `light` во втором роботе.
4. Создать в Property таблицу (InfoTable) в первом и втором роботе.
5. Создать сервис `s_250` в роботе 1, который будет записывать команды в таблицу.

```javascript
me.tablexyzv.RemoveAllRows();
me.tablexyzv.AddRow({x: 10, y: -170, z: 150, v: false}); // Парковка
me.tablexyzv.AddRow({x: 30, y: -256, z: 150, v: false});
me.tablexyzv.AddRow({x: 30, y: -256, z: 0, v: true});
// <.......>
me.line = 0;
```

6. Для робота 2 создать такой же сервис, но со своими координатами.
7. В роботе 1 создать подписку управления светофором 1 (`DataChange` -> `light`)

```javascript
let trafficLightName = "TrafficLightX1";

things[trafficLightName].l1 = false;
things[trafficLightName].l2 = false;
things[trafficLightName].l3 = false;
things[trafficLightName].l4 = false;

if (me.light == 0) 
{
    things[trafficLightName].l1 = true;
} 
else if (me.light == 1) 
{
    things[trafficLightName].l2 = true;
} 
else if (me.light == 2) 
{
    things[trafficLightName].l3 = true;
} 
else if (me.light == 3) 
{
    things[trafficLightName].l4 = true;
}
```

8. В роботе 2 создать такой же сервис но с другим `trafficLightName`
9. В роботе 1 создать подписку сборки (`DataChange` -> `line`)

```javascript
if (me.pause == false) 
{
    if (me.line >= 0 && me.line < me.tablexyzv.getRowCount()) 
    {
        const currentLine = me.tablexyzv[me.line];
        me.x = currentLine.x;
        me.y = currentLine.y;
        me.z = currentLine.z;
        me.v = currentLine.v;
        me.light = 1; pause(2 * 1000);
        me.light = 4; pause(2 * 1000);
        me.line += 1;
    }
    else if (me.line != -1)
    {
        me.line = -1;
        Things["RobotX2"].s_250() 
        // Вызывает сервис выполнения сборки на втором роботе.
        // Чтобы сначала выполнился первый робот а потом второй.
    }
}
```

10. В роботе 2 также создать аналогичную подписку

```javascript
if (Things["RobotX1"].pause == false) 
{
    if (me.line >= 0 && me.line < me.tablexyzv.getRowCount()) 
    {
        const currentLine = me.tablexyzv[me.line];
        me.x = currentLine.x;
        me.y = currentLine.y;
        me.z = currentLine.z;
        me.v = currentLine.v;
        me.light = 1; pause(2 * 1000);
        me.light = 4; pause(2 * 1000);
        me.line += 1;
    }
    else if (me.line != -1)
    {
        me.line = -1;
    }
}
```

11. В роботе 1 создаём подписку на паузу (`DataChange` -> `pause`)

```javascript
if (!me.pause && me.line > -1) 
{
    me.line += 1;
} 

if (!me.pause && Things["RobotX2"].line > -1) 
{
    Things["RobotX2"].line += 1;
}
```
