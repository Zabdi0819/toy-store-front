<template>
  <table class="table table-bordered custom-table">
    <thead class="table-light">
      <tr>
        <th>Id</th>
        <th>Name</th>
        <th>Description</th>
        <th>Maximun age</th>
        <th>Company</th>
        <th>Price</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="p in products" :key="p.id">
        <td>{{ p.id }}</td>
        <td>{{ p.name }}</td>
        <td>{{ p.description }}</td>
        <td>{{ p.ageRestriction ?? '-' }}</td>
        <td>{{ p.company }}</td>
        <td>${{ p.price }}</td>
        <td>
          <div class="container-update">
            <button class="btn-update" @click="$emit('edit', p)">Update</button>
          </div>
          <div class="container-delete mt-2">
            <button class="btn-delete" @click="$emit('delete', p.id)">Delete</button>
          </div>
        </td>
      </tr>
      <tr v-if="products.length === 0">
        <td colspan="7" class="text-center">There are no products.</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    products: { type: Array, required: true }
  }
}
</script>
