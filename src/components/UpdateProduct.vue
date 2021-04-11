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
      <b-form autocomplete="off">
        <b-form-group
          label="Name">
          <b-form-input v-model="form.name" v-validate="{required: true, min: 3}" id="name" name="name" trim></b-form-input>
          <div v-if="submitted" class="error-message">
            {{errors.first('name')}}
          </div>
        </b-form-group>
        <b-form-group
          label="Price ($)">
          <b-form-input v-model="form.price" v-validate="{required: true, numeric: true}" id="price" name="price" trim></b-form-input>
          <div v-if="submitted" class="error-message">
            {{errors.first('price')}}
          </div>              
        </b-form-group>
        <b-form-group
          label="Brand">
          <b-form-input v-model="form.brand" v-validate="{required: true}" id="brand" name="brand" trim></b-form-input>
          <div v-if="submitted" class="error-message">
            {{errors.first('brand')}}
          </div>              
        </b-form-group>
        <b-form-group
          label="Inventory?">
          <div v-if="submitted" class="error-message">
            {{errors.first('inventory-status')}}
          </div>              
          <b-form-radio v-model="form.inventoryStatus" v-validate="{required: true}" name="inventory-status" value="true">In stock</b-form-radio>
          <b-form-radio v-model="form.inventoryStatus" name="inventory-status" value="false">Out of stock</b-form-radio>                                   
        </b-form-group>
      </b-form>    
    </b-modal>
  </div>
</template>

<script>
export default {
  name: 'UpdateProduct',
  props: ['product'],
  data() {
    return {
      modalShow: false,
      form: {
        id: '',
        name: '',
        price: '',
        brand: '',
        inventoryStatus: ''
      },
      submitted: false
    }
  },
  methods: {
    showModal() {
      this.form = {...this.$props.product};
    },
    resetModal() {
      this.form = {};
    },
    async handleSubmit(e) {
      e.preventDefault();

      this.submitted = true;
      let formIsValid = await this.$validator.validate();

      if (formIsValid) {
        this.$emit('updateProduct', 
          {...this.form, inventoryStatus: this.form.inventoryStatus == 'true'});

        this.modalShow = false;
        this.submitted = false;
      }
    }
  }
}
</script>

<style>
</style>
