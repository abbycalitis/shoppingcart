<template>
  <div class="cartTitle"><h1>Your Cart</h1></div>
  <div class="shoppingCart">
    <div v-if="cart.length === 0">Your cart is empty!</div>
    <div v-else>
      <div
        v-for="(item, index) in cart"
        :key="item.product.id"
        class="cartItem"
      >
        <div class="cartItemInfo">
          <div>
            <b>{{ item.product.name }}</b>
            <p>
              ₱{{ item.product.price }}.00 x
              <input
                class="itemQuantity"
                type="number"
                v-model.number="item.quantity"
                min="1"
                v-on:change="updateQuantity(index, item.quantity)"
              /><button class="removeItem" v-on:click="removeItem(index)">
                Remove
              </button>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="total-price">Total Price: ₱ {{ totalPrice }}.00</div>
</template>

<script>
export default {
  name: "ShoppingCart",
  props: {
    cart: Array,
  },
  methods: {
    updateQuantity(index, quantity) {
      this.$emit("updateQuantity", index, quantity);
    },
    removeItem(index) {
      this.$emit("removeItem", index);
    },
  },
  computed: {
    totalPrice() {
      return this.cart.reduce(
        (total, item) => total + item.product.price * item.quantity,
        0
      );
    },
  },
};
</script>

<style>
.cartTitle {
  height: 450px; /* Set a fixed height for the cart */
  width: 25%;
  margin-top: 10px;
  right: 40px; /* Distance from the right side of the viewport */
  z-index: 1000;
  position: fixed;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.shoppingCart {
  height: 400px;
  width: 25%;
  margin-top: 80px;
  margin-left: 10px;
  position: fixed;
  right: 20px;
  z-index: 1000;
  overflow-y: auto;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  border-radius: 10px;
  padding: 20px;
}

.shoppingCart h1 {
  margin-top: 5px; /* Lessen the bottom margin */
}

.removeItem {
  background-color: red;
  color: white;
  border-color: red;
}
.total-price {
  height: 450px; /* Set a fixed height for the cart */
  width: 25%;
  margin-top: 530px;
  right: 40px; /* Distance from the right side of the viewport */
  z-index: 1000;
  position: fixed;
  font-size: 1.5rem;
  font-weight: bold;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
</style>
