<template>
  <h1>Edit Your Project</h1>
  <form @submit.prevent="handleEdit">
    <label for="title">Title:</label>
    <input type="text" v-model="title" id="title" required>
    <label for="details">Details</label>
    <textarea v-model="details" id="details" required></textarea>
    <button>Update</button>
  </form>
</template>

<script>
export default {
  props: ['id'],

  data() {
    return {  
      title: '',
      details: '',
      uri: 'http://localhost:3000/projects/' + this.id
    }
  },

  mounted() {
    fetch(this.uri)
      .then(response => response.json())
      .then(data => {
        this.title = data.title,
        this.details = data.details
      })
  },

  methods: {
    handleEdit() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          title: this.title,
          details: this.details
        })
      })
      .then(() => {
        this.$router.push('/')
      })
      .catch(err => { console.log(err)})
    }
  }
 }
</script>

<style>

</style>