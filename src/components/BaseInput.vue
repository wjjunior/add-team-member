<template>
  <div>
    <b-row class="mt-3">
      <b-col class="label"
        ><label>{{ label }}</label></b-col
      >
      <b-col class="required" v-if="required">Required</b-col>
    </b-row>
    <b-row>
      <input
        @input="$emit('input', $event.target.value)"
        :required="this.required"
        class="form-control"
        v-bind:class="{ 'has-error': !!this.error }"
      />
      <p v-if="error">
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
    required: {
        type: Boolean,
        default: false
    }
  },
};
</script>

<style lang="scss">
@import "../scss/_globals.scss";

p {
  padding: 0 !important;
  text-align: left;
  color: $error;
  font-size: 0.8rem;
  margin-bottom: 0;
}

.has-error {
  border-color: $error !important;
}

.required {
  text-align: end;
  padding-right: 0 !important;
  color: $dark-gray;
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
</style>