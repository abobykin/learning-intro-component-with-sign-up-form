<template>
  <div class="form-column">
    <article class="notification box--rounded">
      <strong>Try it free 7 days </strong>
      then $20/mo. thereafter
    </article>

    <div class="form box--rounded">
      <form @submit.prevent="submit">
        <BaseInput v-model="firstName" label="First Name" type="text" :error="errors.firstName" />
        <BaseInput v-model="lastName" label="Last Name" type="text" :error="errors.lastName" />
        <BaseInput v-model="email" label="Email" type="text" :error="errors.email" />
        <BaseInput v-model="password" label="Password" type="text" :error="errors.password" />

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
    const validations = {
      firstName: (value) => {
        const requiredMessage = 'First name cannot be empty'
        if (value === undefined || value === null) return requiredMessage
        if (!String(value).length) return requiredMessage

        return true
      },
      lastName: (value) => {
        const requiredMessage = 'Last name cannot be empty'
        if (value === undefined || value === null) return requiredMessage
        if (!String(value).length) return requiredMessage

        return true
      },
      email: (value) => {
        if (!value) return 'Email cannot be empty'

        const regex =
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        if (!regex.test(String(value).toLowerCase())) {
          return 'Looks like this is not an email'
        }

        return true
      },
      password: (value) => {
        const requiredMessage = 'Password cannot be empty'
        if (value === undefined || value === null) return requiredMessage
        if (!String(value).length) return requiredMessage

        return true
      }
    }

    const { handleSubmit, errors } = useForm({
      validationSchema: validations
    })

    const { value: firstName } = useField('firstName')
    const { value: lastName } = useField('lastName')
    const { value: email } = useField('email')
    const { value: password } = useField('password')

    const submit = handleSubmit((values) => {
      console.log('submit', values)
    })

    return {
      submit,
      firstName,
      lastName,
      email,
      password,
      errors
    }
  },
  components: {
    BaseInput
  }
}
</script>
