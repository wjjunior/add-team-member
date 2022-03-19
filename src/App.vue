<template>
  <div id="app" class="jumbotron d-flex align-items-center">
    <b-container fluid>
      <b-row class="justify-content-md-center">
        <b-card
          style="max-width: 30rem; height: 40rem; padding: 0"
          title="Add Team Member"
          footer-tag="footer"
        >
          <div
            class="avatar mt-4"
            :style="{ backgroundImage: `url(${form.avatar})` }"
          >
            <div class="upload-avatar" @click="onPickFile">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
                <path
                  d="M421.7 220.3L188.5 453.4L154.6 419.5L158.1 416H112C103.2 416 96 408.8 96 400V353.9L92.51 357.4C87.78 362.2 84.31 368 82.42 374.4L59.44 452.6L137.6 429.6C143.1 427.7 149.8 424.2 154.6 419.5L188.5 453.4C178.1 463.8 165.2 471.5 151.1 475.6L30.77 511C22.35 513.5 13.24 511.2 7.03 504.1C.8198 498.8-1.502 489.7 .976 481.2L36.37 360.9C40.53 346.8 48.16 333.9 58.57 323.5L291.7 90.34L421.7 220.3zM492.7 58.75C517.7 83.74 517.7 124.3 492.7 149.3L444.3 197.7L314.3 67.72L362.7 19.32C387.7-5.678 428.3-5.678 453.3 19.32L492.7 58.75z"
                />
              </svg>
            </div>
          </div>
          <input
            type="file"
            accept="image/*"
            @change="uploadImage"
            hidden
            ref="fileInput"
          />
          <b-form class="register-form">
            <b-row class="mt-3">
              <b-col class="label"><label>Full Name</label></b-col>
              <b-col class="required">Required</b-col>
            </b-row>
            <b-row>
              <b-form-input
                id="input-1"
                v-model="form.fullName"
                required
                v-bind:class="{ 'has-error': !!this.errors.fullName }"
              ></b-form-input>
              <p class="error-message" v-if="errors.fullName">
                {{ this.errors.fullName }}
              </p>
            </b-row>
            <b-row class="mt-3">
              <b-col class="label"><label>Email</label></b-col>
              <b-col class="required">Required</b-col>
            </b-row>
            <b-row>
              <b-form-input
                id="input-1"
                v-model="form.email"
                required
                v-bind:class="{ 'has-error': !!this.errors.email }"
              ></b-form-input>
              <p class="error-message" v-if="errors.email">
                {{ this.errors.email }}
              </p>
            </b-row>
            <b-row class="mt-3">
              <b-col class="label"><label>Job Title</label></b-col>
              <b-col class="required">Required</b-col>
            </b-row>
            <b-row>
              <b-form-input
                id="input-1"
                v-model="form.jobTitle"
                required
                v-bind:class="{ 'has-error': !!this.errors.jobTitle }"
              ></b-form-input>
              <p class="error-message" v-if="errors.jobTitle">
                {{ this.errors.jobTitle }}
              </p>
            </b-row>
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
export default {
  name: "App",
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
      if(this.checkForm()) {
        console.log(JSON.stringify(this.form))
      }
    },
    uploadImage(e) {
      const image = e.target.files[0];
      const reader = new FileReader();
      reader.readAsDataURL(image);
      reader.onload = (e) => {
        this.form.avatar = e.target.result;
      };
    },
    onPickFile() {
      this.$refs.fileInput.click();
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

      return false
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

.avatar {
  width: 150px;
  height: 150px;
  margin: auto;
  border: 0.45rem solid #e4e7eb;
  border-radius: 100%;
  position: relative;
  background-size: 100%;
  background-repeat: no-repeat;
}

.upload-avatar {
  border: 0.45rem solid #e4e7eb;
  background-color: #fff;
  width: 45px;
  height: 45px;
  border-radius: 100%;
  position: absolute;
  bottom: 3rem;
  right: -1.5rem;
  cursor: pointer;
}

.upload-avatar svg {
  width: 1rem;
  padding-top: 10%;
}

.error-message {
  padding: 0 !important;
  text-align: left;
  color: #dd3444;
  font-size: 0.8rem;
  margin-bottom: 0;
}

.has-error {
  border-color: #dd3444 !important;
}

.card-footer {
  background-color: #fff !important;
}
</style>
