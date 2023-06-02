<template>
  <div class="form-column">
    <article class="notification box--rounded">
      <strong>Try it free 7 days </strong>
      then $20/mo. thereafter
    </article>

    <div class="form box--rounded">
      <form @submit.prevent="onSubmit">
        <BaseInput v-model="firstName" label="First Name" type="text" :error="firstNameError" />
        <BaseInput v-model="lastName" label="Last Name" type="text" :error="lastNameError" />
        <BaseInput v-model="email" label="Email" type="text" :error="emailError" />
        <BaseInput v-model="password" label="Password" type="text" :error="passwordError" />

        <button type="submit" class="form__button button--submit">Claim your free trial</button>
      </form>

      <div class="form__notification">
        By clicking the button, you are agreeing to our
        <a href="#">Terms and Services</a>
      </div>
    </div>
  </div>
</template>

<script>
import { useField, useForm } from 'vee-validate'
import BaseInput from '../components/BaseInput.vue'

export default {
  setup() {
    function onSubmit() {
      alert('Submitted')
    }

    const validations = {
      firstName: (value) => {
        const requiredMessage = 'This field is required'
        if (value === undefined || value === null) return requiredMessage
        if (!String(value).length) return requiredMessage

        return true
      },
      lastName: (value) => {
        const requiredMessage = 'This field is required'
        if (value === undefined || value === null) return requiredMessage
        if (!String(value).length) return requiredMessage

        return true
      },
      email: (value) => {
        if (!value) return 'This field is required'

        const regex =
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        if (!regex.test(String(value).toLowerCase())) {
          return 'Looks like this is not an email'
        }

        return true
      },
      password: (value) => {
        const requiredMessage = 'This field is required'
        if (value === undefined || value === null) return requiredMessage
        if (!String(value).length) return requiredMessage

        return true
      }
    }

    useForm({
      validationSchema: validations
    })

    const { value: firstName, errorMessage: firstNameError } = useField('firstName')
    const { value: lastName, errorMessage: lastNameError } = useField('lastName')
    const { value: email, errorMessage: emailError } = useField('email')
    const { value: password, errorMessage: passwordError } = useField('password')

    return {
      onSubmit,
      firstName: firstName,
      firstNameError: firstNameError,
      lastName: lastName,
      lastNameError: lastNameError,
      email: email,
      emailError: emailError,
      password: password,
      passwordError: passwordError
    }
  },
  components: {
    BaseInput
  }
}
</script>
