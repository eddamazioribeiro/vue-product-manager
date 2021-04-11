<template>
  <div>
    <b-button @click="modalShow = !modalShow">
      <i class="fas fa-edit"></i>
    </b-button>
    <b-modal
      v-model="modalShow"
      id="edit-product"
      title="Edit Product"
      @show="showModal"
      @hidden="resetModal"
      @ok="handleSubmit"
    >
    </b-modal>
  </div>
</template>

<script>
export default {
  name: 'UpdateProduct',
  data() {
    return {
      modalShow: false
    }
  },
  methods: {
    showModal() {
      console.log('showModal');
    },
    resetModal() {
      console.log('resetModal');
    },
    handleSubmit(e) {
      e.preventDefault();
      
      console.log('handleSubmit');
    }
  }
}
</script>

<style>
</style>
