<template>
  <div class="row mb-3 mt-3">
    <div class="col">
      <h1 class="mb-3">Add Product</h1>
      <form @submit.prevent="handleAddNewProduct">
        <div class="form-group mt-1 row">
          <label for="input-name" class="col-sm-2 col-2 col-form-label">Name</label>
          <div class="col-sm-10 col-10">
            <input type="text" v-model="name" class="form-control" id="input-name" placeholder="Product's name">
          </div>
        </div>
        <div class="form-group mt-1 row">
          <label for="input-image" class="col-sm-2 col-2 col-form-label">Image Url</label>
          <div class="col-sm-10 col-10">
            <input type="text" v-model="imageUrl" class="form-control" id="input-image" placeholder="Product's image url">
          </div>
        </div>
        <div class="form-group mt-1 row">
          <label for="input-price" class="col-sm-2 col-2 col-form-label">Price</label>
          <div class="col-sm-10 col-10">
            <input type="number" v-model="price" class="form-control" id="input-price" placeholder="Product's price">
          </div>
        </div>
        <div class="form-group mt-1 row">
          <label for="input-stock" class="col-sm-2 col-2 col-form-label">Stock</label>
          <div class="col-sm-10 col-10">
            <input type="number" v-model="stock" class="form-control" id="input-stock" placeholder="Product's stock">
          </div>
        </div>
        <div class="form-group mt-1 row">
          <label for="input-category" class="col-sm-2 col-2 col-form-label">Category</label>
          <div class="col-sm-10 col-10">
            <b-form-select
              v-model="CategoryId"
              :options="categories"
              class="mb-3 form-control"
              value-field="id"
              text-field="name"
              id="input-category"/>
          </div>
        </div>
        <div class="create-btn">
          <button type="submit" class="mt-4 btn btn-primary">Create</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddNewProduct',
  data () {
    return {
      name: '',
      imageUrl: '',
      price: '',
      stock: '',
      CategoryId: ''
    }
  },
  methods: {
    handleAddNewProduct () {
      const { name, imageUrl, price, stock, CategoryId } = this
      this.$store.dispatch('handleAddProduct', {
        name,
        image_url: imageUrl,
        price,
        stock,
        CategoryId
      })
      this.name = ''
      this.imageUrl = ''
      this.price = ''
      this.stock = ''
      this.CategoryId = ''
    },
    getCategories () {
      this.$store.dispatch('fetchCategories')
    }
  },
  created () {
    this.getCategories()
  },
  computed: {
    categories () {
      return this.$store.state.category.categories
    }
  }
}
</script>

<style>

</style>
