# Методы для работы с UI

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

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

```html
<div class="dynamic_basket js-dynamic_basket">
</div>


<script type="text/template" data-template-id="dynamic_basket">
  <div class="dynamic_basket-header">
    ваши покупки
  </div>
  <form action="/cart_items" method="post" data-ajax-cart>
    <input type="hidden" name="_method" value="put">
    <input type="hidden" name="make_order" value="">

  <div class="dynamic_basket-list">
    <% if(order_lines.length == 0){ %>
      <div class="dynamic_basket-empty text-center">
        Корзина пуста
      </div>
    <% } %>
    <% _.forEach(order_lines, function (value){  %>
      <div class="dynamic_item" data-item-id="<%= value.id %>" data-product-id="<%= value.product_id %>">
        <div class="row">
          <div class="cell-4">
            <a href="" class="dynamic_item-image">
              <span class="image-container is-square">
                <img src="<%= value.first_image.medium_url %>">
              </span>
            </a>
          </div>
          <div class="cell-6">
            <div class="dynamic_item-title">
              <%= value.title  %>
            </div>
            <div class="dynamic_item-quantity">
              <%= Shop.money.format(value.sale_price) %> х <%= value.quantity  %>
            </div>

            <div data-quantity class="quantity is-basket">
              <div class="quantity-controls">
                <button data-quantity-change="-1" class="quantity-control bttn-count" type="button">
                  -
                </button>

                <input class="quantity-input" type="text" name="cart[quantity][<%= value.id %>]" value="<%= value.quantity %>" />

                <button data-quantity-change="1" class="quantity-control bttn-count" type="button">
                  +
                </button>
              </div>
            </div>
          </div>
          <div class="cell-2 text-right">
            <button class="dynamic_item-del" data-item-delete="<%= value.id %>">
              &times;
            </button>
          </div>
        </div>
      </div>
    <% }) %>

  </div>

  <% if(order_lines.length > 0){ %>
  <div class="dynamic_basket-total row flex-middle">
    <div class="cell-6 row flex-center">
      итого
    </div>
    <div class="cell-6 row flex-center">
      <%= Shop.money.format(total_price) %>
    </div>
  </div>

  <input type="submit" value="оформить покупки" data-cart-submit class="dynamic_basket-submit bttn-prim">
  <% } %>
  </form>
</script>
```
</details>

---
