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


<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
