<template>
  <div id="sample-table">
    <p v-if="samples.length < 1" class="empty-table">
      No samples
    </p>
    <table v-else>
      <thead>
        <tr>
          <th>Samples name</th>
          <th>Samples email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="sample in samples" :key="sample.id">
          <td v-if="editing === sample.id">
            <input type="text" v-model="sample.name"/>
          </td>
          <td v-else>{{ sample.name }}</td>
          <td v-if="editing === sample.id">
            <input type="text" v-model="sample.email"/>
          </td>
          <td v-else>{{ sample.email }}</td>
          <td v-if="editing === sample.id">
            <button @click="editSample(sample)">Save</button>
            <button class="muted-button" @click="cancelEdit(sample)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(sample)">Edit</button>
            <button @click="$emit('delete:sample', sample.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: "sample-table",
    props: {
      samples: Array,
    },
    data() {
      return {
        editing: null,
      }
    },
    methods: {
      editSample(sample) {
        if (sample.name === '' || sample.email === '') return
        this.$emit('edit:sample', sample.id, sample)
        this.editing = null
      },
      editMode(sample) {
        this.cachedSample = Object.assign({}, sample)
        this.editing = sample.id
      },
      cancelEdit(sample) {
        Object.assign(sample, this.cachedSample)
        this.editing = null;
      }
    }
  }
</script>
<style scoped></style>
