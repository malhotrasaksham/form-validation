<template>
  <div id="app">
    <form @submit.prevent="Submit">
      <div class="formControl" :class="{error: $v.data.email.$error}">
        <input type="text" placeholder="Email" v-model="data.email" @blur="$v.data.email.$touch()">
      </div>
      <div class="formControl" :class="{error: $v.data.age.$error}">
        <input type="text" placeholder="Age" v-model="data.age" @blur="$v.data.age.$touch()">
      </div>
      <div class="formControl">
        <input type="text" placeholder="Pincode">
      </div>
      <div class="formControl" :class="{error: $v.data.gender.$error}">
        <select v-model="data.gender" @blur="$v.data.gender.$touch()">
          <option :value="undefined">--Select--</option>
          <option value="Male">Male</option>
          <option value="Female">Female</option>
        </select>
      </div>
      <div>
        <button :disabled="$v.$invalid" type="submit">Submit</button>
        <button type="submit" @click="SubmitCheck()">Submit</button>
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
      data: {
        email: undefined,
        age: undefined,
        pincode: undefined,
        gender: undefined
      }
    };
  },
  methods: {
    Submit() {
      alert("Invalid: " + this.$v.$invalid);
    },
    SubmitCheck() {
      if (this.$v.$invalid) {
        this.$v.data.$touch();
      }
    }
  },
  validations: {
    data: {
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

