<template>
  <div id="app" class="jumbotron d-flex align-items-center">
    <b-container fluid>
      <b-row class="justify-content-md-center">
        <b-card
          style="max-width: 30rem; height: 40rem; padding: 0"
          title="Add Team Member"
          footer-tag="footer"
        >
          <ImageUploader v-model="form.avatar" />
          <b-form class="register-form">
            <BaseInput
              v-model="form.fullName"
              required
              label="Full Name"
              :error="errors.fullName"
            />
            <BaseInput
              v-model="form.email"
              required
              label="Email"
              :error="errors.email"
            />
            <BaseInput
              v-model="form.jobTitle"
              required
              label="Job Title"
              :error="errors.jobTitle"
            />
          </b-form>
          <template #footer>
            <div class="btn-div">
              <b-button
                variant="primary"
                class="add-btn"
                @click="submit()"
                size="lg"
                >Add Team Member</b-button
              >
            </div>
          </template>
        </b-card>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from 'axios';
import BaseInput from "./components/BaseInput";
import ImageUploader from "./components/ImageUploader";

export default {
  name: "App",
  components: {
    BaseInput,
    ImageUploader,
  },
  data() {
    return {
      errors: {
        fullName: null,
        email: null,
        jobTitle: null,
      },
      form: {
        fullName: "",
        email: "",
        jobTitle: "",
        avatar: null,
      },
    };
  },
  methods: {
    submit() {
      if (this.checkForm()) {
        axios.post('api/v1/my-forml', {
          jsonData: JSON.stringify(this.form)
        })
      }
    },
    checkForm() {
      this.errors = {
        fullName: null,
        email: null,
        jobTitle: null,
      };

      if (this.form.fullName && this.form.email && this.form.jobTitle) {
        return true;
      }

      if (!this.form.fullName) {
        this.errors.fullName = "Name is required.";
      }
      if (!this.form.email) {
        this.errors.email = "Email is required.";
      }
      if (!this.form.jobTitle) {
        this.errors.jobTitle = "Job Title is required.";
      }

      return false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}

.register-form {
  padding-right: 25%;
  padding-left: 25%;
}

.card-body {
  padding: 1rem 0rem !important;
}

.card-title {
  border-bottom: 1px solid #dfdfdf;
  padding-bottom: 1rem;
  font-weight: bold;
}

.btn-div {
  padding-right: 22%;
  padding-left: 22%;
}

.required {
  text-align: end;
  padding-right: 0 !important;
  color: #b2b2b2;
  font-weight: bold;
  font-size: 0.7rem;
  padding-top: 0.5rem;
}

.label {
  text-align: left;
  font-weight: bold;
  font-size: 0.9rem;
  padding-left: 0 !important;
  padding-top: 0.2rem;
}

.add-btn {
  background-color: #2f4d78 !important;
  border-color: #2f4d78 !important;
  color: #fff !important;
  width: 100%;
  font-weight: bold !important;
  font-size: 0.9rem !important;
}

.card-footer {
  background-color: #fff !important;
}
</style>
