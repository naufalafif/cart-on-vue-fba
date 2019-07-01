<template>
  <div>
    <div class="cart">
      <h1>Simple Cart on Vue with FBA</h1>
      <div class="cart-head">
        <div class="info">
        Total Barang : {{cart.reduce((sum, item) => sum + item.quantity ,0)}}
        </div>
        <button class="add-cart" @click="addCart">Tambah Barang</button>
      </div>
      <template v-if='cart.length'>
        <div v-for='item in cart' :key='item.id'>
          <div class="cart-item" >
            <span class="title">{{item.name}}</span>
            <span >
              <button @click="decreaseCartItemQTY(item.id)">-</button>
              {{item.quantity}}
              <button @click="increaseCartItemQTY(item.id)">+</button>
            </span>
            <span class="cart-item-remove" @click="removeCartItem(item.id)">Hapus</span>
          </div>

          -- Harga Satuan :  {{item.price}}
          <br/>
          -- Harga :  {{item.price * item.quantity}}
          <hr/>
        </div>
      </template>
      <p class="total">Total : {{total}}</p>
    </div>

  </div>
</template>

<script>

import { value, computed } from 'vue-function-api'

const deepCopy = (object) => {
  let result = JSON.stringify(object)
  return JSON.parse(result)
}

const DUMMY_ITEM = [
  {
    id: 1,
    name: 'Sepatu',
    quantity: 1,
    price: 1000
  },
  {
    id: 2,
    name: 'Topi',
    quantity: 2,
    price: 1500
  },
  {
    id: 3,
    name: 'Dompet',
    quantity: 3,
    price: 2000
  }
]

export default {
  setup () {
    const cart = value([])
    const total = computed(() => cart.value.reduce((sum, item) => sum + (item.quantity * item.price), 0))
    const addCart = () => {
      const cartId = cart.value.map(item => item.id)
      const filterredItems = DUMMY_ITEM.filter(item => !cartId.includes(item.id))
      if (filterredItems.length) { cart.value = [...cart.value, filterredItems[0]] } else { alert('Barang Habis') }
    }

    const removeCartItem = (id) => {
      cart.value = cart.value.filter(item => item.id !== id)
    }

    const increaseCartItemQTY = (id) => {
      let currentCart = deepCopy(cart.value)
      currentCart = currentCart.map(item => {
        if (item.id === id) { item.quantity++ }
        return item
      })
      cart.value = currentCart
    }

    const decreaseCartItemQTY = (id) => {
      let currentCart = deepCopy(cart.value)
      currentCart = currentCart.map(item => {
        if (item.id === id && item.quantity > 0) { item.quantity-- }
        return item
      })
      cart.value = currentCart
    }

    return {
      cart,
      total,
      addCart,
      decreaseCartItemQTY,
      increaseCartItemQTY,
      removeCartItem
    }
  }
}
</script>
