<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a href="http://localhost:8081/about">
      <button
        type="button"
        class="btn btn-primary">I don't get it. Explain me!
      </button>
    </a>
    <br>
    <br>
    <a href="http://localhost:8081/surveys">
      <button type="button"
              class="btn btn-primary">No time for explanation. Learning by doing!
      </button>
    </a>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
