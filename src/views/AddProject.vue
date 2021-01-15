<template>
  <h1>Stuff to add</h1>
  <form @submit.prevent="handleSubmit">
    <label for="title">Title:</label>
    <input type="text" v-model="title" id="title" required>
    <label for="details">Details</label>
    <textarea v-model="details" id="details" required></textarea>
    <button>Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      details: ''
    }
  },

  methods: {
    handleSubmit() {
      // json server handles the id value for us
      let project = {
        title: this.title,
        details: this.details,
        complete: false
      }
      // fetch request 'POST' etc {title,details,complete,id}
      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      })
      // redirect to home
      .then(() => {
        this.$router.push('/')
      })
      .catch(err => console.log(err))
    }
  }
}
</script>

<style>
  form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }

  label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
  }

  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
  }

  textarea {
    border: 1px solid #fff;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 112px;
  }

  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
    width: 125px;
    font-family: 'Avenir', sans-serif;
  }

</style>