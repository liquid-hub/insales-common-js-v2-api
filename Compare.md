# Сравнение

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

- [Методы](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Compare.md#Методы)
 - [add](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Compare.md#hammer-add)
 - [remove](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Compare.md#hammer-remove)
 - [getCompare](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Compare.md#hammer-getcompare)
 - [update](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Compare.md#hammer-update)

## Интерфейс

> Для быстрого создания интерфейсов в commonjs предусмотрены готовые обработчики форм.

> Обработчики ссылаются на data-атрибуты. В data-атрибуты пробрасывается информация из liquid.

### Кнопки добавить/удалить из сравнения

```html
<button data-compare-add="{{ product.id }}">
  Добавить товар в сравнение
</button>
<button data-compare-delete="{{ product.id }}">
  Удалить из сравнения
</button>
```

---

## Методы

> Методы класса `Compare`

### :hammer: add

> Добавить товар в сравнение

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * @param {number} item id товара
 */
Compare.add({
  item: 123456
});
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Compare.add({
  item: 123456
});
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:compares
* add_items:insales:compares
* update_items:insales:compares
* always:insales:compares


```js
EventBus.subscribe('add_item:insales:compares', function (data) {
  console.log('Товар добавлен в сравнение');
});
```
</details>

---

### :hammer: remove

> Удалить товар из сравнение

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * @param {number} item id товара
 */
Compare.remove({
  item: 123456
});
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Compare.remove({
  item: 123456
});
```
</details>
<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:compares
* remove_item:insales:compares
* update_items:insales:compares
* always:insales:compares


```js
EventBus.subscribe('add_item:insales:compares', function (data) {
  console.log('Товар добавлен в сравнение');
});
```
</details>

---

### :hammer: getCompare

> Получить текущее состояние сравнения

<details>
<summary>:computer: Пример</summary>

```js
var compareState = Compare.getCompare();
console.log(compareState);
```
</details>

---

### :hammer: update

> Обновить состояние сравнения

<details>
<summary>:computer: Пример</summary>

```js
Compare.update();
```
</details>

---



<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
