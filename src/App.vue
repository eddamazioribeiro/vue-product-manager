<template>
  <div id="app">
    <AppHeader />
    <b-container>
      <b-row class="justify-content-center">
        <AddProduct @addProduct="addProduct"/>
        <ListProduct
          @deleteProduct="deleteProduct"
          @updateProduct="updateProduct"
          :products="productList"
        />
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
        this.productList = result.data;
      } catch (err) {
        console.error(err);
      }
    },
    async addProduct(newProduct) {
      try {
        await axios.post('http://localhost:3000/products', newProduct);
        this.getProductList();
      } catch (err) {
        console.log(err);
      }
    },
    async updateProduct(editedProduct) {
      try {
        await axios.put(`http://localhost:3000/products/${editedProduct.id}`, editedProduct);
        this.getProductList();
      } catch (err) {
        console.log(err);
      }
    },
    async deleteProduct(productId) {
      try {
        await axios.delete(`http://localhost:3000/products/${productId}`);
        this.getProductList();
      } catch (err) {
        console.log(err);
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
