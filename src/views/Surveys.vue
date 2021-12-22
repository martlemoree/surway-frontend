<template>
  <h1>Es gibt aktuell {{ surveys.length }} Surveys für dich:</h1>
  <ul class="list-group">
    <div class="col" v-for="survey in surveys" :key="survey.id">
      <li class="list-group-item"> {{ survey.title }} </li>
    </div>
  </ul>
</template>

<script>
export default {
  name: 'Surveys',
  data() {
    return {
      surveys: [],
    };
  },
  mounted() {
    const endpoint = `${process.env.VUE_APP_BACKEND_BASE_URL}/api/v1/surveys`;
    const requestOptions = {
      method: 'GET',
      redirect: 'follow',
    };

    fetch(endpoint, requestOptions)
      .then((response) => { response.json(); })
      .then((result) => {
        result.forEach((survey) => {
          this.surveys.push(survey);
        });
      })
      .catch((error) => { console.log('error', error); });
  },
};
</script>

<style scoped>

</style>
