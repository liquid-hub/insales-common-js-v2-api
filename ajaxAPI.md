# Модуль для работы с API магазина

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

## Методы

> Методы объекта `ajaxAPI`

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

### :hammer: ajaxAPI.shop.client

>  Получение информации о посетителе сайта

<details>
<summary>:computer: Пример</summary>

```js
/*
* Если пользователь залогинен, получим json с акутальной информацией о покупателе
* { status: "ok", client: { // информация о покупателе }}
*
* В случае, если пользователь не залогинен, получим
* { status: "error", message: "Not authorized", url: "/client_account/session/new" }
*/

ajaxAPI.shop.client()
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) })

```
</details>

---

### :hammer: ajaxAPI.shop.review

>  Отправка отзыва к товару

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {Object} review - объект с отзывом. ОБЯЗАТЕЛЬНО
* @param {String} review.author - автор отзыва. ОБЯЗАТЕЛЬНО
* @param {String} review.email - e-mail посетителя. ОБЯЗАТЕЛЬНО
* @param {String} review.content - тело отзыва.ОБЯЗАТЕЛЬНО
* @param {String} review.captcha_solution - капча. ОБЯЗАТЕЛЬНО
* @param {String} productUrl - url товара, к которому хотим оставить отзыв
*/


ajaxAPI.shop.review(review, productUrl)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
var reviewOption = {
  author: 'Пользователь',
  email: 'user@mail.ru',
  content: 'Текст отзыва',
  rating: 5
}
if ($('#recaptcha-token').length) {
    reviewOption['g-recaptcha-response'] = $('#recaptcha-token').val();
}else{
  reviewOption['captcha_solution'] = $('[name="review[captcha_solution]"]').val();
}

ajaxAPI.shop.review(reviewOption, '/collection/shop/product/main')
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---

### :hammer: ajaxAPI.shop.message

>  Отпаравка сообщений

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {Object} message - объект с полями
* @param {string} message.content - тело сообщения. Обязательно
* @param {string} message.from - e-mail, с которого "отправлено" сообщение. Обязательно
* @param {string} message.phone - телефон, указывается в теле письма. По-умолчанию - пустое
* @param {string} message.name - имя, указывается в теле письма. По-умолчанию - пустое.
* @param {string} options.subject - тема письма.
*/

ajaxAPI.shop.message({
  'from': 'json@test.ru',
  'name': 'test is my name',
  'subject': 'test is my subject',
  'content': 'Hello',
  'phone': '+00000000000000'
})
.done(function (onDone) { console.log('onDone: ', onDone) })
.fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.shop.message({
  'from': 'json@test.ru',
  'name': 'test is my name',
  'subject': 'test is my subject',
  'content': 'Hello',
  'phone': '+00000000000000'
})
.done(function (onDone) { console.log('onDone: ', onDone) })
.fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---


<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
