<template>
  <div id="app">
    <AppHeader />
    <b-container>
      <b-row class="justify-content-center">
        <AddProduct />
        <ListProduct />
      </b-row>
    </b-container>
  </div>
</template>

<script>

import AppHeader from './components/AppHeader.vue';
import AddProduct from './components/AddProduct.vue';
import ListProduct from './components/ListProduct.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    AppHeader,
    AddProduct,
    ListProduct
  },
  data() {
    return {
      productList: []
    }
  },
  methods: {
    async getProductList() {
      try {
        let result = await axios.get('http://localhost:3000/products');
        this.productList = result;
      } catch (err) {
        console.error(err);
      }
    }
  },
  mounted() {
    this.getProductList();
  }
}
</script>

<style>
.error-message {
  color: red;
}
</style>
