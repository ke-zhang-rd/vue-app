<template>
  <div id="app" class="small-container">
    <h1>Samples</h1>
    <sample-form @add:sample="addSample" />
    <sample-table :samples="samples"
      @delete:sample=deleteSample
      @edit:sample=editSample
    />
  </div>
</template>

<script>
  import SampleTable from "@/components/SampleTable.vue"
  import SampleForm from "@/components/SampleForm.vue"
  export default {
    name: 'app',
    components: {
      SampleTable,
      SampleForm,
    },
    data() {
      return {
        samples: [
          {
            id: 1,
            name: 'Richard Hendricks',
            email: 'richard@piedpiper.com',
          },
          {
            id: 2,
            name: 'Bertram Gilfoyle',
            email: 'gilfoyle@piedpiper.com',
          },
          {
            id: 3,
            name: 'Dinesh Chugtai',
            email: 'dinesh@piedpiper.com',
          },
        ],
      }
    },
    methods: {
      addSample(sample) {
        const lastId =
          this.samples.length > 0
            ? this.samples[this.samples.length - 1].id
            : 0;
        const id = lastId + 1;
        const newSample = { ...sample, id };

        this.samples = [...this.samples, newSample];
      },
      deleteSample(id) {
        this.samples = this.samples.filter(
          sample => sample.id !== id)
      },
      editSample(id, updatedSample) {
          this.samples = this.samples.map(sample =>
            sample.id === id ? updatedSample : sample)
      }
    }
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>
