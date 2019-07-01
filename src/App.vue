<template>
  <div id="app">
    <Cart/>
  </div>
</template>

<script>
import Cart from './components/Cart.vue'

export default {
  name: 'app',
  components: {
    Cart
  }
}
</script>

<style>
.cart {
    width: 400px;
    margin: auto;
  }

.cart-head {
  padding: 10px;
  display: flex;
}

.cart-head .info {
  flex:1;
}

.cart-head .add-cart {
  flex:1;
}

.cart-item {
  display: flex;
  padding: 10px;
}

.cart-item .title {
  flex:1;
  font-size: 26px;
  font-weight: bold;
}
.cart-item span {
  flex:1;
}

.cart-item .cart-item-remove {
  text-align: right;
  cursor: pointer;
  color: #c73f3f;
  padding: 5px;
}

.total {
  text-align: right;
}
</style>
