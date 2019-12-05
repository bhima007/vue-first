<template>
  <div>
    <h1>This is Form</h1>
    <form @submit.prevent="onSubmit">
      <div class="box">
        <p>{{ $v.confirmPassword }}</p>
        <input type="text" placeholder="email" v-model="email" @blur="$v.email.$touch()">
        <div class="box-error">
          <span v-if="!$v.email.email">It isn't email.</span>
          <span v-if="!$v.email.required && $v.email.$error">It's empty</span>
        </div>

        <input type="text" placeholder="age" v-model="age" @blur="$v.age.$touch()">
        <div class="box-error">
          <span v-if="!$v.age.numeric">It isn't number.</span>
          <span v-if="!$v.age.required && $v.age.$error">It's empty</span>
          <span v-if="!$v.age.min && $v.age.$error">Minimal is {{ $v.age.$params.min.min }}</span>
        </div>

        <input type="password" placeholder="password" v-model="password" @blur="$v.password.$touch()">
        <div class="box-error">
          <span v-if="!$v.password.required && $v.password.$error">It's empty</span>
          <span v-if="!$v.password.min && $v.password.$error">Minimal is {{ $v.password.$params.minLen.min }} character</span>
        </div>

        <input type="password" placeholder="confirmPassword" v-model="confirmPassword" @blur="$v.confirmPassword.$touch()">
        <div class="box-error">
          <span v-if="!$v.sameAs && $v.confirmPassword.$error">It's different</span>
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
      console.log('submitted')
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