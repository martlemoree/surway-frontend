<template>
  <button class="btn btn-success sticky-button"
          data-bs-toggle="offcanvas"
          data-bs-target="#surveys-create-offcanvas"
          aria-controls="#surveys-create-offcanvas">
    <i class="bi bi-person-plus-fill"></i>
  </button>
  <div class="offcanvas offcanvas-end"
       tabindex="-1"
       id="surveys-create-offcanvas"
       aria-labelledby="offcanvas-label">
    <div class="offcanvas-header">
      <h5 id="offcanvas-label">New Survey</h5>
      <button type="button" id="close-offcanvas"
              class="btn-close text-reset"
              data-bs-dismiss="offcanvas"
              aria-label="Close"></button>
    </div>
    <div class="offcanvas-body">
      <form class="text-start needs-validation"
            id="create-survey-form" novalidate>
        <div class="mb-3">
          <label for="title" class="form-label">Title</label>
          <input type="text" class="form-control" id="title" v-model="title" required>
          <div class="invalid-feedback">
            Please provide the title.
          </div>
        </div>
        <div class="mb-3">
          <label for="description" class="form-label">Description</label>
          <input type="text" class="form-control" id="description" v-model="description" required>
          <div class="invalid-feedback">
            Please provide the description.
          </div>
        </div>
        <div class="mb-3">
          <div class="form-check">
            <input class="form-check-input" type="checkbox" id="limited" v-model="limited">
            <label class="form-check-label" for="limited">
              Limited
            </label>
          </div>
        </div>
        <div class="mb-3">
          <label for="limitDate" class="form-label">Limit</label>
          <input type="text" class="form-control" id="limitDate" v-model="limitDate" required>
          <div class="invalid-feedback">
            Please provide the limit.
          </div>
        </div>
        <div v-if="this.serverValidationMessages">
          <ul>
            <li v-for="(message, index) in serverValidationMessages" :key="index"
                style="color: red">
              {{ message }}
            </li>
          </ul>
        </div>
        <div class="mt-5">
          <button class="btn btn-primary me-3" type="submit"
                  @click.prevent="createSurvey">Create</button>
          <button class="btn btn-danger" type="reset">Reset</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CreateSurveyForm',
  data() {
    return {
      title: '',
      description: '',
      limited: '',
      limitDate: '',
      serverValidationMessages: [],
    };
  },
  emits: ['created'],
  methods: {
    async createSurvey() {
      if (this.validate()) {
        const endpoint = `${process.env.VUE_APP_BACKEND_BASE_URL}/api/v1/surveys`;

        const headers = new Headers();
        headers.append('Content-Type', 'application/json');

        const survey = JSON.stringify({
          title: this.title,
          description: this.description,
          limited: this.limited,
          limitDate: this.limitDate,
        });

        const requestOptions = {
          method: 'POST',
          headers,
          body: survey,
          redirect: 'follow',
        };

        const response = await fetch(endpoint, requestOptions);
        await this.handleResponse(response);
      }
    },
    async handleResponse(response) {
      if (response.ok) {
        this.$emit('created', response.headers.get('location'));
        document.getElementById('close-offcanvas').click();
      } else if (response.status === 400) {
        response = await response.json(); // eslint-disable-line no-param-reassign
        response.errors.forEach((error) => {
          this.serverValidationMessages.push(error.defaultMessage);
        });
      } else {
        this.serverValidationMessages.push('Unknown error occured');
      }
    },
    validate() {
      const form = document.getElementById('create-survey-form');
      form.classList.add('was-validated');
      return form.checkValidity();
    },
  },
};
</script>

<style scoped>
.sticky-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  padding: 10px 15px;
  border-radius: 30px;
}
</style>
