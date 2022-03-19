<template>
  <div id="app" class="jumbotron d-flex align-items-center">
    <b-container fluid>
      <b-row class="justify-content-md-center">
        <b-card title="Add Team Member" footer-tag="footer">
          <ImageUploader v-model="form.avatar" />
          <b-form>
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
            <div>
              <b-button variant="primary" @click="submit()" size="lg"
                >Add Team Member
              </b-button>
            </div>
          </template>
        </b-card>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios";
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
        axios.post("api/v1/my-forml", {
          jsonData: JSON.stringify(this.form),
        });
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

<style lang="scss">
@import "./scss/_globals.scss";

#app {
  text-align: center;
  height: 100vh;
}

.card {
  max-width: 30rem !important;
  height: 40rem;
  padding: 0 !important;

  .card-title {
    border-bottom: 0.063rem solid $gray;
    padding-bottom: 1rem;
    font-weight: bold;
  }

  .card-body {
    padding: 1rem 0rem !important;

    form {
      padding-right: 25%;
      padding-left: 25%;
    }
  }

  .card-footer {
    background-color: $white!important;

    div:first-child {
      padding-right: 22%;
      padding-left: 22%;

      button {
        background-color: $dark-blue !important;
        border-color: $dark-blue !important;
        color: $white !important;
        width: 100%;
        font-weight: bold !important;
        font-size: 0.9rem !important;
      }
    }
  }
}
</style>
