<template>
  <div id="app">
    <form @submit.prevent="Submit">
      <div class="formControl" :class="{error: $v.email.$error}">
        <input type="text" placeholder="Email" v-model="email" @blur="$v.email.$touch()">
      </div>
      <div class="formControl" :class="{error: $v.age.$error}">
        <input type="text" placeholder="Age" v-model="age" @blur="$v.age.$touch()">
      </div>
      <div class="formControl">
        <input type="text" placeholder="Pincode">
      </div>
      <div class="formControl" :class="{error: $v.gender.$error}">
        <select v-model="gender" @blur="$v.gender.$touch()">
          <option :value="undefined">--Select--</option>
          <option value="Male">Male</option>
          <option value="Female">Female</option>
        </select>
      </div>
      <div>
        <button :disabled="$v.$invalid" type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
import { required, email, numeric } from "vuelidate/lib/validators";
export default {
  name: "App",
  data() {
    return {
      email: undefined,
      age: undefined,
      pincode: undefined,
      gender: undefined
    };
  },
  methods: {
    Submit() {
      alert(this.$v.$invalid);
    }
  },
  validations: {
    email: {
      email,
      required
    },
    age: {
      numeric,
      required
    },
    gender: {
      required
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
<style scoped>
.formControl {
  padding: 20px;
}
.formControl input {
  outline: none;
}
.formControl.error input,
.formControl.error select {
  border: 1px solid red;
}
</style>

