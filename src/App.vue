<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <!-- update the cart - changed it to be dynamic -->
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>
  <router-view :inventory="inventory" :addToCart="addToCart" />

  <!-- passing props (functions and variables) down to children -->
  <!-- The children can call functions, update the state of the parent component -->
  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />
</template>

<!-- <style scoped></style> -->

<script>
// import Sidebar from './components/Sidebar.vue'
// @ is an alias to /src
import Sidebar from "@/components/Sidebar.vue";
import food from "@/food.json";

// Options Object
export default {
  components: {
    Sidebar,
  },
  data() {
    return {
      showSidebar: false,
      inventory: food,
      cart: {},
    };
  },
  computed: {
    totalQuantity() {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr;
      }, 0);
    },
  },
  methods: {
    addToCart(name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0;
      // need to pass in the index when calling this addToCart function
      // this.inventory[index].quantity -> quantity
      this.cart[name] += quantity;
      // clear the inputs/quantity by setting it to 0
      // this.inventory[index].quantity = 0;
      // console.log(this.cart);
    },
    toggleSidebar() {
      this.showSidebar = !this.showSidebar;
    },
    removeItem(name) {
      delete this.cart[name];
    },
  },
};
</script>
