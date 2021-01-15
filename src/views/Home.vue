<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current"/>
    <h1>Stuff to do</h1>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
    <router-link :to="{ name: 'AddProject' }" class="button">Add Project</router-link>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from "@/components/SingleProject.vue";
import FilterNav from "@/components/FilterNav.vue";

export default {
  name: 'Home',
  components: { SingleProject, FilterNav },

  data() {
    return {
      projects: [],
      current: 'all'
    }
  },

  mounted() {
    fetch('http://localhost:3000/projects')
      .then(response => response.json())
      .then(data => {
        this.projects = data
      })
      .catch(err => console.log(err))
  },

  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(project => {
        return project.id !== id
      })
    },

    handleComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  },

  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      } 
      return this.projects
    }
  }
}
</script>

<style>
  .button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
    text-decoration: none;
    width: 125px;
    text-align: center;
    
  }
</style>
