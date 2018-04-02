# Товар

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

## Интерфейс

> Для быстрого создания интерфейсов в commonjs предусмотрены готовые обработчики форм.

> Обработчики ссылаются на data-атрибуты. В data-атрибуты пробрасывается информация из liquid.

### Назначение атрибутов

<details>
<summary>Подробнее</summary>

| Атрибут               | Назначение                                                                                                                                                | Расположение                                                  |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| data-product-id       | Обязательный атрибут для инициализации товара, принимает id товара                                                                                        | Тег form который является обёрткой для всех полей товара      |
| action                | Обязательный атрибут для формы добавления товара в корзину, принимает url корзины. Тег необходим для отправки формы при отключенном JavaScript в браузере | Тег form который является обёрткой для всех полей товара      |
| data-product-variants | Обязательный атрибут для вывода Option Selectors                                                                                                          | Тег select в котором выведены все модификации товара          |
| data-quantity         | Обязательный атрибут для обёртки кнопок изменения колличества и инпута quantity                                                                           | Внутри формы с атрибутом data-product-id                      |
| data-quantity-change  | Атрибут для кнопок +/-, принимает число                                                                                                                   | Внутри обёртки с атрибутом data-quantity                      |
| data-item-add         | Добавление товара в корзину, для данного атрибута следует использовать тег button\[type="submit"\]                                                        | Внутри формы с атрибутом data-product-id                      |
| name="comment"        | Комментарий к позиции заказа, для работы поля с данным атрибутом комментарии к заказам должны быть включены в бэк-офисе                                   | Input\[type="text"\] внутри формы с атрибутом data-product-id |
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

## Селектор модификаций
## Настройки

## Методы

> Методы класса `Products`

### get

> Получить объект с информацией о товаре

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * @param {number} id id товара
 * @return {Deferred}
 */
Products.get(123456)
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Products.get(123456)
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```
</details>

---

### getList

> Получение списка товаров

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * @param {Array} idList - массив, состоящий из id товаров
 * @return {Deferred}
 */
Products.getList([123456, 123455, 1234454, 123458])
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Products.getList([123456, 123455, 1234454, 123458])
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```
</details>

---

### setConfig

> Обновление настроек

<details>
<summary>:memo: Параметры</summary>

| Property     | Default       | Назначение                                                                                                                                |
|--------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| options      | ```{ 'default': 'option-default' }``` | Через данный объект задаются шаблоны для вывода опций                                                                                     |
| fileUrl      | Пустой объект | Объект для хранения картинок из раздела «Файлы»                                                                                           |
| decimal      | Пустой объект | Колличество символов после запятой, для единиц измерения                                                                                  |
| filtered     | true          | Если значение false, то в шаблоне вывода опций доступно свойство disabled Если значение true, то недоступные опции не выводятся в шаблон. |
| showVariants | true          | При значении false, рендер опций не производится                                                                                          |
| initOption   | true          | Отмечать активные опции при инициализации?                                                                                                |
| useMax       | false         | Использовать максимальное колличество? Если значение true, в quantity невозможно указать колличество больше чем доступно на складе.       |
</details>

<details>
<summary>:computer: Пример</summary>

```js
Products.setConfig({
  showVariants: true,
  hideSelect: true,
  initOption: true,
  fileUrl: {},
  filtered: true,
  selectUnavailable: true
})
```
</details>

---

### getInstance

> Получаем экземпляр класса ProductInstance из jQuery DOM element

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * @param {jQuery DOM element} $node jQuery DOM element например $('.product-cart-control')
 */
Products.getInstance($node)
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```

</details>

<details>
<summary>:computer: Пример</summary>

```js
Products.getInstance($('.product-cart-control'))
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```
</details>

---

### initInstance

> Инициализировать форму товара

<details>
<summary>:memo: Параметры</summary>

```js
/**
 * @param {jQuery DOM element} $node jQuery DOM element например $('.product-cart-control')
 */
Products.initInstance($node)
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```

</details>

<details>
<summary>:computer: Пример</summary>

```js
Products.initInstance($('.product-cart-control'))
  .done(function (onDone) { console.log('onDone', onDone) })
  .fail(function (onFail) { console.log('onFail', onFail) });
```
</details>

---

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
