# Корзина

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>


## Интерфейс

<details>
<summary><h3>Разметка корзины</h3></summary>

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
<details>
<summary><h3>Атрибуты</h3></summary>

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


## Методы

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

### getOrder

> Получить состав корзины

<details>
<summary>:computer: Пример</summary>

```js
var order = Cart.getOrder();
console.log(order);
```
</details>

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
