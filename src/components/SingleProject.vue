<template>
  <div class="projects" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="details = !details">{{ project.title }}</h3>
      <!-- icons, edit etc -->
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id }}">
          <span class="material-icons">edit</span>
        </router-link>
        <span class="material-icons" @click="deleteProject">delete</span>
        <span class="material-icons tick" @click="toggleComplete">grade</span>
      </div>
    </div>
    <div v-if="details" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: [ 'project' ],

  data() {
    return {
      details: false,
      uri: 'http://localhost:3000/projects/' + this.project.id
    }
  },

  methods: {
    deleteProject() {
      fetch(this.uri, { method: 'DELETE'})
        .then(() => this.$emit('delete', this.project.id))
        .catch(err => console.log(err))
    },

    toggleComplete(){
      fetch(this.uri, { 
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete })
      }).then(() => {
        this.$emit('complete', this.project.id)
      }).catch(err => console.log(err))
    }
  }
}
</script>

<style>
  .projects {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0,.05);
    border-left: 6px solid #e90074;
  }

  .projects .tick {
    color: #e90074;
  }

  .complete {
    border-left: 6px solid green;
  }

  .complete .tick {
    color: green;
  }

  .actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  }

  h3 {
    cursor: pointer;
    transition: color .5s;
  }

  h3:hover {
    color: #777;
  }

</style>