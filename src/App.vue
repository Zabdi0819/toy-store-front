<template>
  <div class="container py-4">
    <h1 class="mb-4 text-light text-center">Toy Inventory</h1>

    <!-- Add button -->
    <button class="btn-add mb-4"  @click="openModal()">
      <span class="text">Add new</span>
    </button>

    <!-- Table -->
    <ProductTable 
      :products="products" 
      @edit="openModal" 
      @delete="deleteProduct"
    />

    <!-- Modal -->
    <ProductModal 
      ref="modal"
      :form="form"
      @save="saveProduct"
      @reset="resetForm"
    />

    <!-- Toast -->
    <ProductToast ref="toast" :message="toastMessage" />
  </div>
</template>

<script>
import axios from 'axios'
import { Modal, Toast } from 'bootstrap'
import ProductTable from './components/ProductTable.vue'
import ProductModal from './components/ProductModal.vue'
import ProductToast from './components/ProductToast.vue'

export default {
  name: 'App',
  components: { ProductTable, ProductModal, ProductToast },
  data() {
    return {
      products: [],
      form: {
        id: null,
        name: '',
        description: '',
        ageRestriction: null,
        company: '',
        price: null
      },
      modalInstance: null,
      toastInstance: null,
      toastMessage: ''
    }
  },
  methods: {
    async fetchProducts() {
      try {
        const res = await axios.get('/api/products')
        this.products = res.data
      } catch (err) {
        console.error(err)
      }
    },
    openModal(product = null) {
      if (product) {
        this.form = { ...product }
      } else {
        this.resetForm()
      }
      this.modalInstance.show()
    },
    resetForm() {
      this.form = {
        id: null,
        name: '',
        description: '',
        ageRestriction: null,
        company: '',
        price: null
      }
    },
    async saveProduct() {
      try {
        const { id, ...productData } = this.form

        if (!id) {
          await axios.post('/api/products', productData)
          this.showToast('Product successfully added')
        } else {
          await axios.put(`/api/products/${id}`, productData)
          this.showToast('Product successfully updated')
        }

        await this.fetchProducts()
        this.modalInstance.hide()
      } catch (err) {
        console.error(err)
      }
    },
    async deleteProduct(id) {
      if (!confirm('Are you sure you want to delete this product?')) return
      try {
        await axios.delete(`/api/products/${id}`)
        this.showToast('Product successfully deleted')
        this.fetchProducts()
      } catch (err) {
        console.error(err)
      }
    },
    showToast(message) {
      this.toastMessage = message
      this.$refs.toast.show()
    }
  },
  mounted() {
    this.fetchProducts()
    this.modalInstance = new Modal(this.$refs.modal.$el)
    this.toastInstance = new Toast(this.$refs.toast.$el)
  }
}
</script>
