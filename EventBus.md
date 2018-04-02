# EventBus

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

EventBus (шина событий) предназначена для простого взаимодействия базового функционала с остальными скриптами, не привязываясь при этом к верстке и вспомогательным объектам.

Работает по принципу Pub/Sub (Издатель/Подписчик) и построена на Deferred, что позволяет:

*   привязать к одному событию (Издателю) несколько обработчиков (Подписчиков)
*   обработчики событий сработают, даже если событие произошло раньше того, как мы к нему привязали обработчик.
*   не важен порядок объявления Издателя и Подпсичиков

Работа с шиной производится через объект EventBus.

- [subscribe](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/EventBus.md#subscribe)
- [publish](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/EventBus.md#publish)
- [logger.add](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/EventBus.md#loggeradd)

### subscribe

> Подписаться на событие

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * eventId {String} название события
 * callback {function} функция обработчик события
 */
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
EventBus.subscribe('event_id', function (data) {
  console.log(data)
});
```
</details>

---

### publish

> Публикация события

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * eventId {String} название события
 * data {Object} любой тип данных, преимущественно `Object`
 */
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
EventBus.publish('event_id', {
  isTest: true,
  title: 'Test',
  status: 'ok'
});
```
</details>

---

### logger.add

> Добавление логера для компонента

<details>
<summary>:memo: Параметры</summary>

Список компонентов:

- cart
- product
- search
- compares

```js
/**
 * componentTitle {String} название компонента
 */
```
</details>

<details>
<summary>:computer: Пример</summary>

```js
EventBus.logger.add('cart')
EventBus.logger.add('product')
```
</details>


<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
