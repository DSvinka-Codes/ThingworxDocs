# Проектирование взаимодействий элементов приложени

Диограмма последовательности - Диаграмма которая отображает взаимодействие между элементами программной системы, обозначая линию их жизни и передаваемые сообщения.

Данная диаграмма содержит последовательность сообщений передаваемых объектами и упорядоченных по времени их возникновения.

## Элементы диаграммы последовательности

#### Фрейм

<img src="../.gitbook/assets/file.excalidraw (4).svg" alt="" class="gitbook-drawing">

#### Линия жизни (Life line) объектов и спецификация выполнения (Execution Specification) соответственно

<img src="../.gitbook/assets/file.excalidraw (3).svg" alt="" class="gitbook-drawing">

#### Сообщения (Messages) соответственно: Асинхронное сообщение; Вызов операции; Ответ

<img src="../.gitbook/assets/file.excalidraw (5).svg" alt="" class="gitbook-drawing">

#### Потерянное сообщение и найденное сообщение соответственно

<img src="../.gitbook/assets/file.excalidraw (6).svg" alt="" class="gitbook-drawing">

## Схема потоков обработки данных системы управления

<img src="../.gitbook/assets/file.excalidraw (7).svg" alt="" class="gitbook-drawing">

***

<figure><img src="../.gitbook/assets/Untitled Diagram.drawio.png" alt=""><figcaption></figcaption></figure>

***

<figure><img src="../.gitbook/assets/Untitled Diagram.drawio (2).png" alt=""><figcaption></figcaption></figure>

В случае, если необходимо отразить **роль объектов в системе**, подчеркнув, например, что сообщения приходят от граничных и внешних объектов системы, используются следующие специальные обозначения объектов

Actor - действущее лицо\
Boundary Object - граничный объект\
Control Object - управляющий объект, процесс

<img src="../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

<img src="../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">
