<template>
  <div class="card-wrapper">
    <v-card class="card">
      <v-form ref="form" lazy-validation>
        <v-text-field
          label="Email"
          name="email"
          type="email"
          :rules="$v.email.email"
          v-model.trim.lazy="$v.email.$model"
        />
        <v-text-field label="Password" name="password" type="password" />
        <v-btn>Login</v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { required, email, minLength } from "vuelidate/lib/validators";

export default Vue.extend({
  name: "Home",

  validations: {
    email: {
      required,
      email: {
        email,
      },
    },

    password: {
      required,
      minLength: minLength(6),
    },
  },
});
</script>

<style lang="scss">
.card {
  width: 75%;
  padding: 2rem 0.5rem;

  &-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
  }
}
</style>
