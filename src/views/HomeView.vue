<template>
  <v-container fluid class="d-flex align-center justify-center home__container">
    <v-card class="home__card">
      <v-form ref="form" autocomplete="off" lazy-validation @submit.prevent="handleSubmit">
        <v-text-field
          :error-messages="emailErrors"
          label="Email"
          name="email"
          type="email"
          v-model.trim="email"
          required
          @input="$v.email.$reset()"
          @blur="$v.email.$reset()"
        />
        <v-text-field
          :error-messages="passwordErrors"
          label="Password"
          name="password"
          type="password"
          v-model.trim="password"
          required
          @input="$v.password.$reset()"
          @blur="$v.password.$reset()"
        />
        <v-btn type="submit">Login</v-btn>
      </v-form>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import Vue from "vue";
import { validationMixin } from "vuelidate";
import { required, email, minLength } from "vuelidate/lib/validators";

export default Vue.extend({
  mixins: [validationMixin],

  data: () => ({
    email: "",
    password: "",
  }),

  validations: {
    email: {
      required,
      email,
    },

    password: {
      required,
      minLength: minLength(6),
    },
  },

  methods: {
    handleSubmit(event: SubmitEvent) {
      this.$v.$touch();

      if (this.$v.$invalid) {
        return;
      }

      this.$router.push("/products");
    },
  },

  computed: {
    emailErrors() {
      const errors: string[] = [];
      if (!this.$v.email.$dirty) return errors;
      if (!this.$v.email.email) errors.push("Email should be valid");
      if (!this.$v.email.required) errors.push("Email is required");

      return errors;
    },

    passwordErrors() {
      const errors: string[] = [];

      if (!this.$v.password.$dirty) return errors;
      if (!this.$v.password.minLength) errors.push("Password should have at least 6 characters");
      if (!this.$v.password.required) errors.push("Password is required");

      return errors;
    },
  },
});
</script>

<style lang="scss" scoped>
.home {
  &__container {
    height: 100%;
  }

  &__card {
    width: 100%;
    max-width: 30rem;
    padding: 1rem 0.5rem;
  }
}
</style>
