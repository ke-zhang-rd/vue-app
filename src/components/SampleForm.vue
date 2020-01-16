<template>
  <div id="sample-form">
    <form @submit.prevent="handleSubmit">
      <label>Sample name</label>
      <input
        ref="first"
        type="text" 
        :class="{ 'has-error': submitting && invalidName }"
        v-model="sample.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      />
      <label>Sample Email</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        v-model="sample.email"
        @focus="clearStatus"
      />
      <p v-if="error && submitting" class="error-message">
        ❗Please fill out all required fields
      </p>
      <p v-if="success" class="success-message">
         ✅ Sample successfully added
      </p>
      <button>Add Sample</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'sample-form',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        sample: {
          name: "",
          email: "",
        }
      }
    },
    computed: {
      invalidName() {
        return this.sample.name === ""
      },
      invalidEmail() {
        return this.sample.email === ""
      },
    },
    methods: {
      handleSubmit() {
        this.submitting = true
        this.clearStatus()
        if (this.invalidName || this.invalidEmail) {
          this.error = true
          return
        }
        this.$emit('add:sample', this.sample)
        this.$refs.first.focus()
        this.sample = {
          name: '',
          email: '',
        }
        this.error = false
        this.success = true
        this.submitting = false
      },
      clearStatus() {
        this.error = false
        this.success = false
      },
    },
  }

</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>
