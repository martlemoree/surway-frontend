<template>
  <h1>Aktuell {{ surveys.length }} Surveys für dich:</h1>
  <div class="container-fluid">
    <survey-list :surveys="this.surveys"></survey-list>
  </div>
  <create-survey-form @created="addSurvey"></create-survey-form>
</template>

<script>
import SurveyList from '@/components/SurveyList.vue';
import CreateSurveyForm from '@/components/CreateSurveyForm.vue';

export default {
  name: 'Surveys',
  components: {
    SurveyList,
    CreateSurveyForm,
  },
  data() {
    return {
      surveys: [],
    };
  },
  methods: {
    addSurvey(surveyLocation) {
      const endpoint = process.env.VUE_APP_BACKEND_BASE_URL + surveyLocation;
      const requestOptions = {
        method: 'GET',
        redirect: 'follow',
      };

      fetch(endpoint, requestOptions)
        .then((response) => {
          response.json();
        })
        .then((survey) => {
          this.surveys.push(survey);
        })
        .catch((error) => {
          console.log('error', error);
        });
    },
  },
  mounted() {
    const endpoint = `${process.env.VUE_APP_BACKEND_BASE_URL}/api/v1/surveys`;
    const requestOptions = {
      method: 'GET',
      redirect: 'follow',
    };

    fetch(endpoint, requestOptions)
      .then((response) => {
        console.log(response);
        return response.json();
      })
      .then((result) => {
        result.forEach((survey) => {
          this.surveys.push(survey);
        });
      })
      .catch((error) => {
        console.log('error', error);
      });
  },
};
</script>

<style scoped>

</style>
