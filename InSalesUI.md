# Методы для работы с UI

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

## Методы

> Методы объекта `InSalesUI`

### :hammer: InSalesUI.initAjaxInstance

> Инициализация формы корзины

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {jquery} jquery объект
*/

InSalesUI.initAjaxInstance($(".js-dynamic_basket"));
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
EventBus.subscribe("update_items:insales:cart", function(cart) {
  $(".js-dynamic_basket").html(Template.render(cart, "dynamic_basket"));
  InSalesUI.initAjaxInstance($(".js-dynamic_basket"));
});
```
</details>

---
