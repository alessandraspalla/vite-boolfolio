<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  mounted() {
    axios.get('http://127.0.0.1:8000/api/v1/project-index')
      .then(res => {
        console.log(res);
      })
      .catch(err => {
        console.log(err);
      })
  }
}
</script>

<template>
  <h1>Funziona</h1>
</template>

<style scoped></style>
