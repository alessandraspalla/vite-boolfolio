<script>
import axios from 'axios';

export default {
  name: 'ProjectCard',
  data() {
    return {
      projects: [],
      links: []
    }
  },
  methods: {
    changePage(newPage) {
      axios.get(newPage)
        .then(res => {
          const data = res.data;
          console.log(data);

          this.projects = data.projects.data;
          this.links = data.projects.links;
        })
        .catch(err => {
          console.log(err);
        })
    }
  },
  mounted() {
    axios.get('http://127.0.0.1:8000/api/v1/project-index')
      .then(res => {
        const data = res.data;
        console.log(data);

        this.projects = data.projects.data;
        this.links = data.projects.links;
      })
      .catch(err => {
        console.log(err);
      })
  }
}
</script>

<template>
  <h1>Projects</h1>
  <ul>
    <li v-for="project in projects" :key="project.id">
      {{ project.name }}
    </li>
  </ul>
  <div class="pages mt-5">
    <div v-for="(link, idx) in links" :key="idx" class="page mx-2 btn" v-html="link.label"
      :class="(link.active ? 'btn-success' : 'btn-warning') + '' + (link.url === null ? 'd-none text-light' : '')"
      @click="changePage(link.url)">
    </div>
  </div>
</template>

<style scoped></style>
