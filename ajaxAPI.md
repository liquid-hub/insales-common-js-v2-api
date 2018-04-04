# Модуль для работы с API магазина

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

## Методы

> Методы объекта `ajaxAPI.cart`

### :hammer: ajaxAPI.cart.add

> Добавление товаров в корзину

<details>
<summary>:memo: Параметры</summary>

```js
/*
* var items = {
*   123456: 1,
*   123457: 3,
*   123450: 100
* };
*
* var options = {
*   comments: { 123456: 'Ваш комментарий' },
*   coupon: 'test'
* }
*/

ajaxAPI.cart.add(items, options)
  .done(function (onDone) { console.log ('onDone: ', onDone) })
  .fail(function (onFail) { console.log ('onFail:', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.cart.add({
    123456: 1,
    123457: 3,
    123450: 100
  }, {
    comments: { 123456: 'Ваш комментарий' },
    coupon: 'test'
  })
  .done(function (onDone) { console.log ('onDone: ', onDone) })
  .fail(function (onFail) { console.log ('onFail:', onFail) });
```
</details>

---

### :hammer: ajaxAPI.cart.get

> Получение состава корзины

<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.cart.get()
  .done(function (onDone) { console.log ('onDone: ', onDone) })
  .fail(function (onFail) { console.log ('onFail:', onFail) });
```
</details>

---

### :hammer: ajaxAPI.cart.remove

> Удаление товара из корзины

<details>
<summary>:computer: Пример</summary>

```js
/**
 * @param {Number} variant_id - id модификации
 */
ajaxAPI.cart.remove(123123)
  .done(function (onDone) { console.log ('onDone: ', onDone) })
  .fail(function (onFail) { console.log ('onFail:', onFail) });
```
</details>

---

### :hammer: ajaxAPI.cart.update

>  Обновление состава корзины.

Позволяет:
 * обновить состав корзины
 * удалить несколько позиций
 * добавить несколько позиций
 * изменить кол-во товаров позиции
 * установить комментарии к позициям


<details>
<summary>:memo: Параметры</summary>

```js
/*
  * @param {Object} items - набор пар {variant_id: quantity, ...}. Если quantity = 0, то позиция удаляется из корзины, в противном случае устанавливается указанное кол-во
  * @param {Object} options - дополнительные поля: comments, coupon
  * @param {Object} options.comments - объект с комментариями вида {variant_id: comment, ...}
  * @param {String} options.coupon - название купона
*/

var items = {
  123456: 1,
  123457: 3,
  123450: 100
};

var options = {
  comments: { 123456: 'Ваш комментарий' },
  coupon: 'test'
}

ajaxAPI.cart.update(items, optins)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
var items = {
  123456: 1,
  123457: 3,
  123450: 100
};

var options = {
  comments: { 123456: 'Ваш комментарий' },
  coupon: 'test'
}

ajaxAPI.cart.update(items, optins)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---




<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
