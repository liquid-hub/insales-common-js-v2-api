# Модуль для работы с API магазина

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

- Корзина
  - [add](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicartadd)
  - [get](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicartget)
  - [remove](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicartremove)
  - [update](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicartupdate)
- Магазин
  - [client](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapishopclientget)
  - [review](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapishopreview)
  - [comment](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapishopcomment)
  - [message](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapishopmessage)
- Товар
  - [getList](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapiproductgetList)
  - [get](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapiproductget)
- Категория
  - [get](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicollectionget)
- Оформление заказа
  - [order](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicheckoutorder)
- Сравнение
  - [add](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicompareadd)
  - [remove](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicompareremove)
  - [get](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md#hammer-ajaxapicompareget)
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

### :hammer: ajaxAPI.shop.client.get

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

ajaxAPI.shop.client.get()
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

### :hammer: ajaxAPI.shop.comment

>  Отправка комментария к статье

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {Object} comment - объект с комментарием. ОБЯЗАТЕЛЬНО
* @param {String} comment.author - автор комментария. ОБЯЗАТЕЛЬНО
* @param {String} comment.email - e-mail посетителя. ОБЯЗАТЕЛЬНО
* @param {String} comment.content - тело комментария.ОБЯЗАТЕЛЬНО
* @param {String} comment.captcha_solution - капча. ОБЯЗАТЕЛЬНО
* @param {String} articleUrl - url статьи, к которому хотим оставить отзыв
*/


ajaxAPI.shop.comment(comment, articleUrl)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
var commentOption = {
  author: 'Пользователь',
  email: 'user@mail.ru',
  content: 'Текст'
}
if ($('#recaptcha-token').length) {
    reviewOption['g-recaptcha-response'] = $('#recaptcha-token').val();
}else{
  reviewOption['captcha_solution'] = $('[name="review[captcha_solution]"]').val();
}

ajaxAPI.shop.comment(commentOption, '/blogs/blog/aktsiya')
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

### :hammer: ajaxAPI.product.getList

>  Получение информации о списке товаров

<details>
<summary>:memo: Параметры</summary>

```js
/*
* Важно! Отсутствует поле "подробное описание".
*
* @param {array} ids - список id товаров, за раз моно получить информацию не более чем о 100 товарах
*/

ajaxAPI.product.getList([123456,123457,123458,123459])
  .done(function (onDone) {console.log('onDone: ', onDone) })
  .fail(function (onFail) {console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.product.getList([123456,123457,123458,123459])
  .done(function (onDone) {console.log('onDone: ', onDone) })
  .fail(function (onFail) {console.log('onFail: ', onFail) });
```
</details>

---

### :hammer: ajaxAPI.product.get

>  Получение информации о товаре

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {number} id - id товара
*/

ajaxAPI.product.get(123456)
  .done(function (onDone) {console.log('onDone: ', onDone) })
  .fail(function (onFail) {console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.product.get(123456)
  .done(function (onDone) {console.log('onDone: ', onDone) })
  .fail(function (onFail) {console.log('onFail: ', onFail) });
```
</details>

---

### :hammer: ajaxAPI.collection.get

>  Получение информации о коллекции

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {string} handle - пермалинк коллекции, объязателен.
* @param {Object} filter - объект с выбранными параметрами для фильтрации
* @param {Object} pager - объект с настройками пагинации
* @param {number} pager.page_size - размер разбивки на страницы
* @param {number} pager.page - номер страницы, по которой получаем информацию
*/

var filter = {
  price_min: 4000,
  price_max: 10000
};

var pager = {
  page_size: 25,
  page: 2
}

ajaxAPI.collection.get('collection_handle', filter, pager)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
var filter = {
  price_min: 4000,
  price_max: 10000
};

var pager = {
  page_size: 25,
  page: 2
}

ajaxAPI.collection.get('collection_handle', filter, pager)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---

### :hammer: ajaxAPI.checkout.order

>  Оформление заказа с указанием способа оплаты и доставки. Важно - все поля обязательны для заполнения.

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {Object} client - объект с полями {email: почта, name: имя, phone: телефон}
* @param {string} client.email - почта
* @param {string} client.name - ФИО
* @param {string} client.phone - телефон
* @param {Object} order - объект с обязательными полями
* @param {number} order.delivery - id способа доставки
* @param {number} order.payment - id способа оплаты
*/

ajaxAPI.checkout.order(client, order)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.checkout.order({
  email: 'user@mail.ru',
  name: 'user',
  phone: '79879991122'
  }, {
  delivery: 1111111,
  payment: 2222222
})
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---

### :hammer: ajaxAPI.compare.add

>  Добавление товара в сравнение

<details>
<summary>:memo: Параметры</summary>

```js
/*
 * @param {number} id - id товара, добавляемого в сравнение
*/

ajaxAPI.compare.add(123456)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.compare.add(123456)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---

### :hammer: ajaxAPI.compare.remove

>  Удаление товара из сравнения

<details>
<summary>:memo: Параметры</summary>

```js
/*
 * @param {number} id - id товара, удаляемого из списка.
*/

ajaxAPI.compare.remove(123456)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.compare.remove(123456)
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---

### :hammer: ajaxAPI.compare.get

>  Получение списка сравнения

<details>
<summary>:computer: Пример</summary>

```js
ajaxAPI.compare.get()
  .done(function (onDone) { console.log('onDone: ', onDone) })
  .fail(function (onFail) { console.log('onFail: ', onFail) });
```
</details>

---


<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
