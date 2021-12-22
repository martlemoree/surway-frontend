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
      surveys: [
        {
          id: 1,
          title: 'Corona Maßnahmen',
          desciption: 'Bewertung der Strenge der Corona Maßnahmen',
          limited: true,
          limitDate: '31.12.2021',
        },
        {
          id: 2,
          title: 'Klimaerwärmung',
          description: 'Wie viel Wissen haben Sie über Klimaerwärmung?',
          limited: false,
          limitDate: null,
        },
        {
          id: 4,
          title: 'Inflationsängste',
          description: 'Themen zur ansteigenden Inflation',
          limited: true,
          limitDate: '31.03.2022',
        },
      ],
    };
  },
};
</script>

<style scoped>

</style>
