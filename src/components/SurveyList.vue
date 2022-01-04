<template>
  <ul class="list-group">
    <div class="col" v-for="survey in surveys" :key="survey.id">
      <survey-answer-form :survey="survey"></survey-answer-form>
        <li class="list-group-item">
          {{ survey.title }}
        </li>
    </div>
  </ul>
</template>

<script>
import SurveyAnswerForm from '@/components/SurveyAnswerForm.vue';

export default {
  name: 'SurveyList',
  components: {
    SurveyAnswerForm,
  },
  props: {
    surveys: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>

</style>
