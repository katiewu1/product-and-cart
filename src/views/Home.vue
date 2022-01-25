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
        <div
          v-for="(product, i) in inventory.slice(0, 3)"
          :key="product.id"
          class="card"
        >
          <div class="card-title">{{ product.name }}</div>
          <div class="card-body">
            <i class="icofont-10x icofont-{{ product.icon }}"></i>
            <form>
              <div class="row">
                <div class="cell">
                  <label>Type:</label>
                </div>
                <div class="cell">
                  <em>{{ product.type }}</em>
                </div>
              </div>
              <div class="row">
                <div class="cell">
                  <label>Price:</label>
                </div>
                <div class="cell">${{ product.price.USD.toFixed(2) }}</div>
              </div>
              <div class="row">
                <div class="cell">
                  <label>Quantity:</label>
                </div>
                <div class="cell">
                  <!-- v-model (string) -> v-model.number (number), v-model.number="inventory.carrots" -->
                  <!-- v-model.number="inventory[i].quantity" -> v-model.number="product.quantity" -->
                  <input type="number" v-model.number="product.quantity" />
                </div>
              </div>
            </form>
          </div>
          <div class="card-footer">
            <!-- @click="addToCart('carrots', inventory.carrots)" -->
            <!-- @click="addToCart('carrots')" -->
            <button @click="addToCart(product.name, i)" class="btn btn-light">
              Add to cart
            </button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import food from "../food.json";
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      inventory: food,
    };
  },
  components: {},
};
</script>
