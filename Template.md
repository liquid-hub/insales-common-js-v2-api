# Lodash шаблоны

Компонет «Template» отвечает за хранение и получение шаблонов написанных на шаблонизаторе библиотеки lodash.

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

- [Методы](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Template.md#Методы)
  - [load](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Template.md#hammer-load)
  - [render](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Template.md#hammer-render)

## Разметка

> Шаблоны записываются в тег script с обязательными атрибутами `type`, `data-template-id`.

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

## Методы

> Методы класса `Template`

### :hammer: load

> Загрузка нового шаблона в список

<details>
<summary>:memo: Параметры</summary>

```js
/**
* @param {string} template_body - верстка шаблона
* @param {string} template_id - название шаблона
 */
Template.load('<button class="button button--click_me"><%= title %></button>', 'test-button')
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Template.load('<button class="button button--click_me"><%= title %></button>', 'test-button')
```
</details>

---

### :hammer: render

> Загрузка нового шаблона в список

<details>
<summary>:memo: Параметры</summary>

```js
/**
* @param {Object} templateData - информация для шаблонизатора
* @param {string} template_id - название шаблона
 */
$(targetNode).html(Template.render({ title: 'Click me!' }, 'test-button' ));
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
$(targetNode).html(Template.render({ title: 'Click me!' }, 'test-button' ));
```
</details>

---


<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
