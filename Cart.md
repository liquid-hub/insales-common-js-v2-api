# Корзина

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>


- [Интерфейс](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#%D0%98%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81)
  - [Назначение-атрибутов](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#Назначение-атрибутов)
  - [Разметка-товара](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#Разметка-товара)
  - [Разметка-корзины](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#Разметка-корзины)
- [Методы](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#Методы)
  - [add](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#add)
  - [delete](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#delete)
  - [clear](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#clear)
  - [remove](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#remove)
  - [set](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#set)
  - [setCoupon](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#setcoupon)
  - [order.get](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#orderget)
  - [order.getItemByID](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md#ordergetitembyid)


## Интерфейс

> Для быстрого создания интерфейсов в commonjs предусмотрены готовые обработчики форм.

> Обработчики ссылаются на data-атрибуты. В data-атрибуты пробрасывается информация из liquid.

### Назначение атрибутов

<details>
<summary>Подробнее</summary>

| Атрибут              | Назначение                                                                      | Расположение                                              |
|----------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------|
| data-cart-form       | Обязательный атрибут для тега form                                              | Тег form для корзины                                      |
| data-item-id         | Обязательный атрибут для позиций в корзине. Атрибут принимает id позиции.       | Обертка для позиции в корзине                             |
| data-product-id      | Обязательный атрибут для инициализации товара. В атрибут передаётся id товара.  | Обертка для позиции в корзине                             |
| data-item-delete     | Удаление из корзины                                                             | Обертка для позиции в корзине                             |
| data-cart-update     | Обновление корзины                                                              | Внутри обёртки с атрибутом data-cart-form                 |
| data-cart-update     | Обновление корзины                                                              | Внутри обёртки с атрибутом data-cart-form                 |
| data-cart-clear      | Очищение корзины                                                                | Внутри обёртки с атрибутом data-cart-form                 |
| data-coupon-submit   | Отправка купона                                                                 | Внутри обёртки с атрибутом data-cart-form                 |
| data-quantity        | Обязательный атрибут для обёртки кнопок изменения колличества и инпута quantity | Внутри обертки с атрибутом data-product-id и data-item-id |
| data-quantity-change | Атрибут для кнопок +/-, принимает число                                         | Внутри обёртки с атрибутом data-quantity                  |
</details>

---

### Разметка товара

<details>
<summary>Подробнее</summary>

```twig
<form action="{{ cart_url }}" method="post" data-product-id="{{ product.id }}">
  {% if product.show_variants? %}
    <select name="variant_id" data-product-variants>
      {% for variant in product.variants %}
        <option value="{{ variant.id }}">{{ variant.title | escape }}</option>
      {% endfor %}
    </select>
  {% else %}
    <input type="hidden" name="variant_id" value="{{product.variants.first.id}}" >
  {% endif %}
  <input type="text" name="comment" value="">
  <div data-quantity>
    <input type="text" name="quantity" value="1" />
    <span data-quantity-change="-1">-</span>
    <span data-quantity-change="1">+</span>
  </div>
  <button type="submit" data-item-add>
    Добавить в корзину
  </button>
</form>
```

</details>

---

### Разметка корзины

<details>
<summary>Подробнее</summary>

```twig
<form action="{{ cart_url }}" method="post" data-cart-form>
  <input type="hidden" name="_method" value="put">
  <input type="hidden" name="make_order" value="">

  {% for item in cart.items %}
    <div data-product-id="{{ item.product.id }}" data-item-id="{{ item.id }}">
      <div data-quantity>
        <input type="text" name="cart[quantity][{{ item.id }}]" value="{{ item.quantity }}">
        <span data-quantity-change="-1">-</span>
        <span data-quantity-change="1">+</span>
      </div>
      <span data-item-delete="{{ item.id }}">X</span>
    </div>
  {% endfor %}

  <div>
    <label> Купон </label>
    <input type="text" name="cart[coupon]" value="{{ cart.coupon }}" />
    <input type="button" value="Применить" data-coupon-submit/>
  </div>

  <input type="submit" value="Оформить" data-cart-submit>
  <button data-cart-clear>Очистить</button>
  <button data-cart-update>Обновить</button>
</form>
```
</details>

---
---

## Методы

> Методы класса `Cart`

### add

> Добавить в корзину заданное кол-во товаров

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * items {Object} хэш таблица добавляемых товаров. Ключ id варианта, значение кол-во.
 * comments {Object} комментарий к позиции заказа. Ключ id варианта, значение текст комментария.
 * coupon {string} купон
 */
{
  items: {
    123456: 2,
    123457: 1
  },
  comments: {
    123457: 'Мой комментарий'
  },
  coupon: 'Мой купон'
}
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Cart.add({
  items: {
    123456: 2,
    123457: 1
  },
  comments: {
    123457: 'Мой комментарий'
  },
  coupon: 'Мой купон'
});
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:cart
* add_items:insales:cart
* update_items:insales:cart
* always:insales:cart


```js
EventBus.subscribe('add_items:insales:cart', function (data) {
  console.log('Товар добавлен');
});
```
</details>

---

### delete

> Удалить позиции из корзины

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * items {Array} массив id вариантов к удалению
 */
 {
   items: [160549240, 160549242]
 }
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Cart.delete({
  items: [160549240, 160549242]
})
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:cart
* delete_items:insales:cart
* update_items:insales:cart
* always:insales:cart


```js
EventBus.subscribe('delete_items:insales:cart', function (data) {
  console.log('Товары удалены');
});
```
</details>

---

### clear

> Полностью очистить корзину


<details>
<summary>:computer: Пример</summary>

```js
Cart.clear();
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:cart
* clear_items:insales:cart
* update_items:insales:cart
* always:insales:cart


```js
EventBus.subscribe('clear_items:insales:cart', function (data) {
  console.log('Корзина очищена');
});
```
</details>

---

### remove

> Удадить из корзины заданное кол-во товаров

<details>
<summary>:memo: Параметры</summary>

```js
/**
* items {Array}  объект с параметрами variant_id: quantity
*/
{
  items: {
    138231315: 1,
    138231316: 1
  }
}
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Cart.remove({
  items: {
    138231315: 1,
    138231316: 1
  }
})
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:cart
* remove_items:insales:cart
* update_items:insales:cart
* always:insales:cart


```js
EventBus.subscribe('remove_items:insales:cart', function (data) {
  console.log('Товары удалены');
});
```
</details>

---

### set

> Устанавливает кол-во товаров в корзине для каждой позиции

<details>
<summary>:memo: Параметры</summary>

```js
/**
* items {Array}  объект с параметрами variant_id: quantity
*/
{
  items: {
    138231315: 1,
    138231316: 1
  }
}
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Cart.set({
  items: {
    138231315: 1,
    138231316: 1
  }
})
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:cart
* set_items:insales:cart
* update_items:insales:cart
* always:insales:cart


```js
EventBus.subscribe('set_items:insales:cart', function (data) {
  console.log('Корзина обновлена');
});
```
</details>

---

### setCoupon

> Устанавливает купон

<details>
<summary>:memo: Параметры</summary>

```js
/**
* coupon {string}  код купона
*/
{
  coupon: 'Мой купон'
}
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Cart.setCoupon({
  coupon: 'Мой купон'
})
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:cart
* set_coupon:insales:cart
* update_items:insales:cart
* always:insales:cart


```js
EventBus.subscribe('set_coupon:insales:cart', function (data) {
  console.log('Добавлен купон');
});
```
</details>

---

### order.get

> Получить состав корзины

<details>
<summary>:computer: Пример</summary>

```js
var order = Cart.order.get();
console.log(order);
```
</details>

---

### order.getItemByID

> Получить информацию о позиции по id

<details>
<summary>:computer: Пример</summary>

```js
var item = Cart.order.getItemByID(138231315);
console.log(item);
```
</details>


<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
