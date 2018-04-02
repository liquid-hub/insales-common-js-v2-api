# insales-common-js-v2


# Корзина

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
