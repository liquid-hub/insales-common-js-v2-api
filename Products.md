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

### Привязка шаблона модификации к опции

> В методе `setConfig` нужно передать объект options в виде `имя опции: id шаблона`

<details>
<summary>Подробнее</summary>

```js
Products.setConfig({
  options: {
    'Цвет': 'option-image',
    'Размер': 'option-radio',
    'Материал': 'option-select',
    'Жесткий диск': 'option-span'
  }
});
```

Пример шаблона

```html
<script type="text/template" data-template-id="option-span">
  <div class="<%= classes.option %> is-span">
    <label class="<%= classes.label %>"><%= title %></label>
    <div class="<%= classes.values %>">
      <% _.forEach(values, function (value){ %>
        <button class="<%= value.classes.all %> is-span"
          <%= value.controls %>
          <%= value.state %>
        >
          <%= value.title %>
        </button>
      <% }) %>
    </div>
  </div>
</script>
```
</details>

---

### Передать изображения для шаблона селектора модификаций

> Ссылки формируются в виде `значение свойства + .png | file_url`

<details>
<summary>Подробнее</summary>

```twig
<script>
  {% comment %}
    создание объекта с картинками из файлов для collection
  {% endcomment %}
  if (!fileUrl) {
   var fileUrl = {}
  }
  {% assign option_title  = 'Цвет' %}
  {% assign collection_handle  = 'all' %}
  {% assign image_format  = '.png' %}
  {% for option_name in collections[collection_handle].options %}
    {% if option_name.title == option_title %}
      {% for option_value in option_name.values %}
        {% capture fileName %}{{option_value.title | replace: ' ',  '_' }}{{image_format}}{% endcapture %}
        {% assign fileURL = fileName | file_url  %}
        {% if fileURL %}
          fileUrl['{{ option_value.title | downcase }}'] = '{{ fileURL }}';
        {% endif %}
      {% endfor %}
    {% endif %}
  {% endfor %}
</script>

<script>
  {% comment %}
    создание объекта с картинками из файлов для product
  {% endcomment %}
  if (!fileUrl) {
   var fileUrl = {}
  }
  {% assign option_title  = 'цвет' %}
  {% assign image_format  = '.png' %}
  {% for option in product.options %}
    {% assign option-title = option.title | downcase %}
    {% if option-title == option_title %}
     {% for value in option.values %}
       {% capture fileName %}{{value.title | replace: ' ',  '_'}}{{image_format}}{% endcapture %}
       {% assign fileURL = fileName | downcase | file_url  %}
       {% if fileURL %}
        fileUrl['{{ value.title | downcase }}'] = encodeURI('{{ fileURL }}');
       {% endif %}
     {% endfor %}
    {% endif %}
  {% endfor %}
</script>

<script>
  Products.setConfig({
    fileUrl: (typeof fileUrl == 'undefined') ? {} : fileUrl
  });
</script>
```
</details>

---

### Шаблоны для селектора модификаций

<details>
<summary>select</summary>

```html
<script type="text/template" data-template-id="option-select">
  <div class="<%= classes.option %> is-select">
    <label class="<%= classes.label %>"><%= title %></label>
    <select class="<%= classes.values %>" data-option-bind="<%= option.id %>">
      <% _.forEach(values, function (value){ %>
        <option
          <%= value.controls %>
          <%= value.state %>
        >
          <%= value.title %>
        </option>
      <% }) %>
    </select>
  </div>
</script>
```
</details>
<details>
<summary>span</summary>

```html
<script type="text/template" data-template-id="option-span">
  <div class="<%= classes.option %> is-span">
    <label class="<%= classes.label %>"><%= title %></label>
    <div class="<%= classes.values %>">
      <% _.forEach(values, function (value){ %>
        <button class="<%= value.classes.all %> is-span"
          <%= value.controls %>
          <%= value.state %>
        >
          <%= value.title %>
        </button>
      <% }) %>
    </div>
  </div>
</script>
```
</details>
<details>
<summary>radio</summary>

```html
<script type="text/template" data-template-id="option-radio">
  <div class="<%= classes.option %> is-radio">
    <label class="<%= classes.label %>"><%= title %></label>

    <div class="<%= classes.values %>">
      <% _.forEach(values, function (value){ %>
        <label class="<%= value.classes.all %> is-radio">
          <input class="<%= value.classes.state %>"

            type="radio"
            name="<%= handle %>"

            <%= value.state %>
            <%= value.controls %>
          >
          <span><%= value.title %></span>
        </label>
      <% }) %>
    </div>
  </div>
</script>
```
</details>
<details>
<summary>image</summary>

```html
<script type="text/template" data-template-id="option-image">
  <div class="<%= classes.option %> option-<%= option.handle %>">
    <label class="<%= classes.label %>"><%= title %></label>
    <div>
      <% _.forEach(option.values, function (value){ %>
        <span
          data-option-bind="<%= option.id %>"
          data-value-position="<%= value.position %>"
          class="option-image
          <% if (option.selected == value.position & initOption) { %>active<% } %>
          <% if (value.disabled) { %>disabled<% } %>"
        >
          <% if (images[value.name]) { %>
            <img src="<%= images[value.name].small_url %>" alt="<%= value.title %>">
          <% }else{ %>
            <span><%= value.title %></span>
          <% } %>
        </span>
      <% }) %>
    </div>
  </div>
</script>
```
</details>

---

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
  fileUrl: (typeof fileUrl == 'undefined') ? {} : fileUrl,
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
