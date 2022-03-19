<template>
  <div id="app" class="jumbotron d-flex align-items-center">
    <b-container fluid>
      <b-row class="justify-content-md-center">
   <b-card style="max-width: 30rem; height: 40rem; padding: 0;" title="Add Team Member">
      <b-form class="register-form">
        <b-row class="mt-4">
          <b-col class="label"><label>Full Name</label></b-col>
          <b-col class="required">Required</b-col>
        </b-row>
        <b-row>
          <b-form-input
          id="input-1"
          v-model="form.username"
          required
        ></b-form-input>
        </b-row>
        <b-row class="mt-4">
          <b-col class="label"><label>Email</label></b-col>
          <b-col class="required">Required</b-col>
        </b-row>
        <b-row>
          <b-form-input
          id="input-1"
          v-model="form.email"
          required
        ></b-form-input>
        </b-row>
        <b-row class="mt-4">
          <b-col class="label"><label>Job Title</label></b-col>
          <b-col class="required">Required</b-col>
        </b-row>
        <b-row>
          <b-form-input
          id="input-1"
          v-model="form.jobTitle"
          required
        ></b-form-input>
        </b-row>
      </b-form>
       <div class="mt-3 pt-4 btn-div">
          <b-button variant="primary" class="add-btn" @click="login()">Add Team Member</b-button>
        </div>
   </b-card>
   </b-row>
   </b-container>
  </div>
  
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      form: {
        username: "",
        email: "",
        jobTitle: ""
      }
    }
  },
  method: {
    login() {
      console.log('login')
    }
  }
}
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
  border-bottom: 1px solid #DFDFDF;
  padding-bottom: 1rem;
  font-weight: bold;
}

.btn-div {
  border-top: 1px solid #DFDFDF;
  padding-right: 22%;
  padding-left: 22%;
}

.required {
  text-align: end;
  padding-right: 0 !important;
  color: #B2B2B2;
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
  background-color: #2F4D78 !important;
  border-color: #2F4D78 !important;
  color: #fff !important;
  width: 100%;
  font-weight: bold !important;
  font-size: 0.9rem !important;
}
</style>
