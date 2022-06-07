<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject @deleteProject="deleteProject($event)" :project="project" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from "../components/SingleProject.vue"

export default {
  name: "Home",
  data() {
    return {
      projects: []
    }
  },
  methods: {
    deleteProject (id) {
      this.projects = this.projects.filter((val) => val.id !== id)
    }
  },
  components: { SingleProject },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
};
</script>
