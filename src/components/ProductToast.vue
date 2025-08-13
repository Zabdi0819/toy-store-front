<!-- ProductToast.vue -->
<template>
  <div 
    ref="toastEl" 
    class="toast align-items-center text-bg-success border-0" 
    role="alert" 
    aria-live="assertive" 
    aria-atomic="true"
  >
    <div class="d-flex">
      <div class="toast-body">
        {{ message }}
      </div>
      <button 
        type="button" 
        class="btn-close btn-close-white me-2 m-auto" 
        data-bs-dismiss="toast" 
        aria-label="Close"
      ></button>
    </div>
  </div>
</template>

<script>
import { Toast } from 'bootstrap'

export default {
  name: 'ProductToast',
  props: {
    message: String
  },
  mounted() {
    this.toast = new Toast(this.$refs.toastEl, {
      delay: 3000, // 3 segundos
      autohide: true
    })
  },
  methods: {
    show() {
      this.toast.show()
    }
  }
}
</script>

<style scoped>
.toast {
  position: fixed;
  bottom: 1rem;
  right: 1rem;
  z-index: 1055;
}
</style>
