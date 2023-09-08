# Товар

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

- [Интерфейс](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Интерфейс)
  - [Назначение атрибутов](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Назначение-атрибутов)
  - [Разметка товара](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Разметка-товара)
- [События](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#События)
- [Селектор модификаций](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Селектор-модификаций)
  - [Привязка шаблона модификации к опции](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Привязка-шаблона-модификации-к-опции)
  - [Передать изображения для шаблона селектора модификаций](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Передать-изображения-для-шаблона-селектора-модификаций)
  - [Шаблоны для селектора модификаций](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Шаблоны-для-селектора-модификаций)
- [Методы](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#Методы)
  - [get](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#hammer-get)
  - [getList](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#hammer-getlist)
  - [setConfig](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#hammer-setconfig)
  - [getInstance](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#hammer-getinstance)
  - [initInstance](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md#hammer-initinstance)


## Интерфейс

> Для быстрого создания интерфейсов в commonjs предусмотрены готовые обработчики форм.

> Обработчики ссылаются на data-атрибуты. В data-атрибуты пробрасывается информация из liquid.

### Назначение атрибутов

| Атрибут               | Назначение                                                                                                                                                | Расположение                                                  |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| data-product-id       | Обязательный атрибут для инициализации товара, принимает id товара                                                                                        | Тег form который является обёрткой для всех полей товара      |
|data-product-without-cache| Отключить кеширование информации о данном товаре| Тег с атрибутом data-product-id | 
| action                | Обязательный атрибут для формы добавления товара в корзину, принимает url корзины. Тег необходим для отправки формы при отключенном JavaScript в браузере | Тег form который является обёрткой для всех полей товара      |
| data-product-variants | Обязательный атрибут для вывода Option Selectors                                                                                                          | Тег select в котором выведены все модификации товара          |
| data-quantity         | Обязательный атрибут для обёртки кнопок изменения колличества и инпута quantity                                                                           | Внутри формы с атрибутом data-product-id                      |
| data-quantity-change  | Атрибут для кнопок +/-, принимает число                                                                                                                   | Внутри обёртки с атрибутом data-quantity                      |
| data-item-add         | Добавление товара в корзину, для данного атрибута следует использовать тег button\[type="submit"\]                                                        | Внутри формы с атрибутом data-product-id                      |
| name="comment"        | Комментарий к позиции заказа, для работы поля с данным атрибутом комментарии к заказам должны быть включены в бэк-офисе                                   | Input\[type="text"\] внутри формы с атрибутом data-product-id |
|data-product-json="{{ product\|json\|escape }}"|Передать данные о товаре через ликвид. Это может ускорить отображение селектора модификаций|Тег form который является обёрткой для всех полей товара|

Для установки минимального значения в инпуте кол-ва товара укажите атрибут data-min
```twig
  <div data-quantity data-min="10">
    <input type="text" name="quantity" value="10" />
    <span data-quantity-change="-10">-</span>
    <span data-quantity-change="10">+</span>
  </div>
```

---

### Разметка товара

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

---

## События

| Событие                           | Описание                                                              |
|-----------------------------------|-----------------------------------------------------------------------|
| before:insales:product            | Событие срабатывает перед любым взаимодействием с компонетом продукта |
| always:insales:product            | Событие срабатывает после любого взаимодействия с компонетом продукта |
| change_quantity:insales:product   | Обновление кол-ва в продукте                                          |
| unchange_quantity:insales:product | Если введено кол-во больше доступного                                 |
|overload:quantity:insales:product| Событие срабатывает когда с помощью +/- накликали до максимального значения  quantity (Работает если вы используете параметр useMax)|
|max:quantity:insales:product| Cрабатывает всегда когда в инпуте установлено максимальное кол-во, даже при загрузке страницы (Работает если вы используете параметр useMax)|
| update_variant:insales:product    | Обновление варианта в продукте                                        |

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

> [!WARNING]
> В примерах ниже используется библиотека lodash, которая создаёт глобальную
> переменную с именем `_` (нижнее подчеркивание). При использовании кода из примеров,
> необходимо самостоятельно подключить библиотеку [lodash](https://lodash.com/). 

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
          <% if (!value.available) { %>disabled<% } %>"
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

<details>
<summary>preview</summary>

```html
<script type="text/template" data-template-id="option-preview">
<div class="<%= classes.option %> option-<%= option.handle %>" is-span is-preview">
  <label class="<%= classes.label %>"><%= title %></label>
  <div class="<%= classes.values %>">
    <% _.forEach(values, function (value){ %>
      <button class="<%= value.classes.all %> is-span is-preview"
        <%= value.controls %>
        <%= value.state %>
      >
        <% if(value.imageFromVariant){ %>
          <img width="40px" src="<%= value.imageFromVariant.medium_url %>" alt="<%= value.titleWithoutQuotes %>" title="<%= value.titleWithoutQuotes %>">
        <% }else{ %>
          <span><%= value.title %></span>
        <% } %>
      </button>
    <% }) %>
  </div>
</div>

</script>
```
</details>

---

## Методы

> Методы класса `Products`

### :hammer: get

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

### :hammer: getList

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

### :hammer: setConfig

> Обновление настроек

Параметры

| Property     | Default       | Назначение                                                                                                                                |
|--------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| options      | ```{ 'default': 'option-default' }``` | Через данный объект задаются шаблоны для вывода опций                                                                                     |
| fileUrl      | Пустой объект | Объект для хранения картинок из раздела «Файлы»                                                                                           |
| decimal      | Пустой объект | Колличество символов после запятой, для единиц измерения                                                                                  |
| filtered     | true          | Если значение true, то недоступные опции не выводятся в шаблон. |
| disableHideItem     | false          | Показывает недоступные варианты товаров, даже если в бек-офисе они отключены |
| selectUnavailable     | true          | Разрешить выбирать недоступный вариант (актуально если `filtered: false`) |
| allowUnavailable     | false          | Разрешить выбирать первым недоступный вариант |
| showVariants | true          | При значении false, рендер опций не производится                                                                                          |
| initOption   | true          | Отмечать активные опции при инициализации?                                                                                                |
| useMax       | false         | Использовать максимальное колличество? Если значение true, в quantity невозможно указать колличество больше чем доступно на складе.       |

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

### :hammer: getInstance

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

### :hammer: initInstance

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
