<template>
  <div class="container mt-5">
    <form v-if="!formSubmitted" @submit.prevent="submitForm" class="border p-4 rounded">
      <div class="mb-3">
        <label for="plan" class="form-label">Plan:</label>
        <textarea id="plan" v-model="plan" class="form-control" rows="10" required></textarea>
      </div>

      <div>
        <label for="query" class="form-label">Query:</label>
        <textarea id="query" v-model="query" class="form-control" rows="5" required></textarea>
      </div>

      <button type="submit" class="btn btn-outline-secondary active mt-3">Submit</button>
    </form>
  </div>
  <div id="app" class="d-flex" v-if="formSubmitted">
    <Pev2Wrapper :plan-source="plan" :plan-query="query" @back="goBackToHome"></Pev2Wrapper>
  </div>
</template>

<script>
import Pev2Wrapper from './components/Pev2Wrapper.vue';
import "pev2/dist/style.css";

export default {
  name: "App",
  components: {
    Pev2Wrapper
  },
  data() {
    return {
      plan: '',
      query: '',
      formSubmitted: false
    };
  },
  methods: {
    submitForm() {
      if (this.plan && this.query) {
        this.formSubmitted = true;
      } else {
        alert('Please fill in both fields.');
      }
    },
    handleBeforeUnload(event) {
      if (this.formSubmitted || (this.plan && this.query)) {
        event.preventDefault();
        event.returnValue = ''; // Required for Chrome
      }
    }
  },
  mounted() {
    window.addEventListener('beforeunload', this.handleBeforeUnload);
  },
  beforeDestroy() {
    window.removeEventListener('beforeunload', this.handleBeforeUnload);
  }
};
</script>