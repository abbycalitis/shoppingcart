<template>
  <div id="app" class="app-container">
    <ProductList :products="products" @addToCart="addToCart"></ProductList>
    <ShoppingCart
      :cart="cart"
      @removeItem="removeItem"
      @updateQuantity="updateQuantity"
      class="shoppingCart"
    ></ShoppingCart>
  </div>
</template>

<script>
import ProductList from "./components/Products.vue";
import ShoppingCart from "./components/Cart.vue";

export default {
  name: "App",
  components: {
    ProductList,
    ShoppingCart,
  },
  data() {
    return {
      products: [
        { id: 1, name: "Halo-Halo", price: 55 },
        { id: 2, name: "Saging con Yelo", price: 20 },
        { id: 3, name: "Mais con Yelo", price: 20 },
        { id: 4, name: "Banana Cue", price: 20 },
        { id: 5, name: "Taho", price: 30 },
        { id: 6, name: "Buko Pandan", price: 30 },
        { id: 7, name: "Leche Flan", price: 70 },
        { id: 8, name: "Ube", price: 60 },
        { id: 9, name: "Coke Float", price: 55 },
        { id: 10, name: "Ice Cream", price: 30 },
      ],
      cart: [],
    };
  },
  methods: {
    addToCart(product) {
      const existingItem = this.cart.find(
        (item) => item.product.id === product.id
      );
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cart.push({ product: product, quantity: 1 });
      }
    },
    removeItem(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index, quantity) {
      if (quantity <= 0) {
        this.removeItem(index);
      } else {
        this.cart[index].quantity = quantity;
      }
    },
  },
};
</script>

<style>
.app-container {
  display: flex;
  flex-wrap: wrap;
}
</style>
