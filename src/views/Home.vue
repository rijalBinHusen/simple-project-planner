<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :currentFilter="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject 
        @deleteProject="deleteProject($event)" 
        :project="project" 
        @completeProject="completeProject($event)"
        />
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */ 
// @ is an alias to /src
import SingleProject from "../components/SingleProject.vue"
import FilterNav from "../components/FilterNav.vue"

export default {
  name: "Home",
  data() {
    return {
      projects: [],
      current: 'all',
    }
  },
  computed: {
    filteredProjects() {
      if(this.current == 'completed') { 
        return this.projects.filter((val) => val.complete)
       }
      if(this.current == 'ongoing') {
        return this.projects.filter((val) => !val.complete)
      }
      return this.projects
      
    }
  },
  methods: {
    deleteProject (id) {
      this.projects = this.projects.filter((val) => val.id !== id)
    },
    completeProject(id) {
      let currentProject = this.projects.find((val) => val.id === id)
      currentProject.complete = !currentProject.complete
    }
  },
  components: { SingleProject, FilterNav },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
};
</script>
