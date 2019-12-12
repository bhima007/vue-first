<template>
  <div>
    <h1>This is Form</h1>
    <form @submit.prevent="onSubmit">
      <div class="box">
        <input type="text" placeholder="Email" v-model="email" @change="$v.email.$touch()">
        <div class="box-error">
          <span v-if="!$v.email.email">It isn't email.</span>
          <span v-if="!$v.email.required && $v.email.$error">It's empty</span>
        </div>

        <input type="text" placeholder="Age" v-model="age" @change="$v.age.$touch()">
        <div class="box-error">
          <span v-if="!$v.age.numeric">It isn't number.</span>
          <span v-if="!$v.age.required && $v.age.$error">It's empty</span>
          <span v-if="!$v.age.min && $v.age.$error">Minimal is {{ $v.age.$params.min.min }}</span>
        </div>

        <input type="password" placeholder="Password" v-model="password" @change="$v.password.$touch()">
        <div class="box-error">
          <span v-if="!$v.password.required && $v.password.$error">It's empty</span>
          <span v-if="!$v.password.minLen && $v.password.$error">Minimal is {{ $v.password.$params.minLen.min }} character</span>
        </div>

        <input type="password" placeholder="Confirm Password" v-model="confirmPassword" @change="$v.confirmPassword.$touch()">
        <div class="box-error">
          <span v-if="!$v.sameAs && $v.confirmPassword.$error">It's different</span>
        </div>

        <div>
          <button type="submit">Submit</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { required, email, numeric, minValue, minLength, sameAs } from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      email: '',
      age: null,
      password: '',
      confirmPassword: ''
    }
  },
  validations: {
    email: {
      required,
      email
    },
    age: {
      required,
      numeric,
      min: minValue(17)
    },
    password: {
      required,
      minLen: minLength(6)
    },
    confirmPassword: {
      sameAs: sameAs('password')
    }
  },
  methods: {
    onSubmit () {
      const data = {
        email: this.email,
        age: this.age,
        password: this.password,
        confirmPassword: this.confirmPassword
      }
      if (this.$v.$invalid === false) {
        console.log('submitted', data);
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  justify-content: center;
}
.box {
  display: flex;
  flex-direction: column;
  width: 200px;
}
.box-error {
  display: flex;
  flex-direction: column;
  height: 14px;
  font-size: 12px;
  color: firebrick;
}
</style>