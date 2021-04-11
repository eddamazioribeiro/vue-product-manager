<template>
  <b-col md="4" class="m-3">
    <div>
      <b-card header="List Product">
        <b-card-group deck>
          <b-card
            v-for="prod in products" :key="prod.id"
            :border-variant="prod.inventoryStatus ? 'success' : 'danger'"
            align="left"
            style="min-width: 50%;"
            class="m-3"
            >
            <small>
              <b-badge class="mb-2" :variant="prod.inventoryStatus ? 'success' : 'danger'">
                {{prod.inventoryStatus ? 'AVAILABLE' : 'OUT OF STOCK'}}
              </b-badge>
            </small>
            <b-card-text><strong>Name: </strong>{{prod.name}}</b-card-text>
            <b-card-text><strong>Price: </strong>${{prod.price}}</b-card-text>
            <b-card-text><strong>Brand: </strong>{{prod.brand}}</b-card-text>
            <hr/>
            <b-row  align="center">
              <b-col>
                <b-button variant="danger" @click="deleteProduct(prod.id)">
                  <i class="fas fa-trash"></i>
                </b-button>
              </b-col>
              <b-col>
                <UpdateProduct :product="prod" @updateProduct="updateProduct"/>
              </b-col>
            </b-row>
          </b-card>
        </b-card-group>
      </b-card>
    </div>
  </b-col>
</template>

<script>
import UpdateProduct from './UpdateProduct.vue';

export default {
  props: ['products'],
  components: {
    UpdateProduct
  },
  methods: {
    deleteProduct(productId) {
      this.$emit('deleteProduct', productId);
    },
    updateProduct(editedProduct) {
      this.$emit('updateProduct', editedProduct);
    }
  }
}
</script>

<style>
</style>
