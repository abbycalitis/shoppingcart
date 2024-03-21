<template>
  <div class="productHeader">
    <h1>List of Products</h1>
    <div class="productList">
      <div class="productBox">
        <div v-for="product in products" :key="product.id" class="productCard">
          <div class="productDetails">
            <h3 class="productName">{{ product.name }}</h3>
            <h4 class="productPrice">₱{{ product.price }}.00</h4>
            <button class="addToCart" v-on:click="addToCart(product)">
              Add to Cart
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductList",
  props: {
    products: Array,
  },
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    },
  },
};
</script>

<style scoped>
.productList {
  justify-content: flex-start;
  width: 70%;
}

.productHeader {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.productHeader h1 {
  margin-bottom: 10px; /* Lessen the bottom margin */
  margin-left: 20px; /* Add margin to the left */
}
.productBox {
  margin-left: 50px;
  display: flex;
  flex-wrap: wrap;
}
.productCard {
  margin: 20px;
  padding: 25px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2); /* Add a shadow for depth */
  height: 200px;
  width: 200px;
  box-sizing: border-box;
  border-radius: 10px; /* Rounded corners */
  text-align: center;
  font-size: 1rem;
}
</style>
