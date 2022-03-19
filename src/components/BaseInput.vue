<template>
  <div>
    <b-row class="mt-3">
      <b-col class="label"
        ><label>{{ label }}</label></b-col
      >
      <b-col class="required">Required</b-col>
    </b-row>
    <b-row>
      <input
        @input="$emit('input', $event.target.value)"
        required
        class="form-control"
        v-bind:class="{ 'has-error': !!this.error }"
      />
      <p class="error-message" v-if="error">
        {{ this.error }}
      </p>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "BaseInput",

  props: {
    label: {
      type: String,
      required: true,
    },
    error: {
      type: String,
    },
  },
};
</script>

<style>
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
</style>