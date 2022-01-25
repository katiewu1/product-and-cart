/* eslint-disable semi */
<template>
  <div class="home">
    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food</h1>
      </div>
    </div>

    <main class="wrapper">
      <h2>Recommended</h2>

      <div class="recommended">
        <!-- Loop over every item in the inventory and with slice only show the first three products -->
        <!-- v-for="(product, i) in inventory.slice(0,3)" :key="i" -->
        <ProductCard
          v-for="(product, index) in inventory.slice(0, 3)"
          :key="product.id"
          class="card"
          :index="index"
          :product="product"
          :addToCart="addToCart"
        />
      </div>
    </main>
  </div>
</template>

<script>
import ProductCard from "@/components/ProductCard.vue";
// import ProductCard from "../components/ProductCard.vue";
export default {
  name: "Home",
  props: ["inventory", "addToCart"],
  components: {
    ProductCard,
  },
};
</script>

ProductCard
