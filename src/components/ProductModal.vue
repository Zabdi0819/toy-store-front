<template>
  <div class="modal fade" id="productModal" tabindex="-1" ref="modal">
    <div class="modal-dialog">
      <div class="modal-content">
        <form @submit.prevent="$emit('save')">
          <div class="modal-header">
            <h5 class="modal-title">{{ form.id ? 'Update Product' : 'New Product' }}</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
          </div>
          <div class="modal-body">
            <div class="mb-3">
              <label class="form-label">Name</label>
              <input type="text" class="form-control" v-model="form.name" required maxlength="50">
            </div>
            <div class="mb-3">
              <label class="form-label">Company</label>
              <input type="text" class="form-control" v-model="form.company" required maxlength="50">
            </div>
            <div class="mb-3">
              <label class="form-label">Description</label>
              <input type="text" class="form-control" v-model="form.description" maxlength="100">
            </div>
            <div class="mb-3">
              <label class="form-label">Maximun age</label>
              <input type="number" class="form-control" v-model.number="form.ageRestriction" min="0" max="100">
            </div>
            <div class="mb-3">
              <label class="form-label">Price</label>
              <input type="number" class="form-control" v-model.number="form.price" required min="1" max="1000" step="0.01">
            </div>
          </div>
          <div class="modal-footer">
            <div class="container-cancel">
              <button type="button" class="btn-cancel" data-bs-dismiss="modal" @click="$emit('reset')">Cancel</button>
            </div>
            <div class="container-save">
              <button type="submit" class="btn-save" >Save</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    form: { type: Object, required: true }
  }
}
</script>
