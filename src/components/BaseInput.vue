<script>
import SetupFormComponent from '@/utils/SetupFormComponent'
import UniqueID from '@/utils/UniqueID'
import BaseErrorMessage from '../components/BaseErrorMessage.vue'

export default {
  components: {
    BaseErrorMessage
  },
  props: {
    label: {
      type: String,
      default: ''
    },
    error: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    }
  },
  setup(props, context) {
    const { updateValue } = SetupFormComponent(props, context)
    const uuid = UniqueID().getID()

    return {
      updateValue,
      uuid
    }
  }
}
</script>

<template>
  <div class="form__field--block" :class="{ error }">
    <input
      v-bind="{
        ...$attrs,
        onInput: updateValue
      }"
      class="form__field"
      :id="uuid"
      :value="modelValue"
      :placeholder="label"
      :aria-describedby="error ? `${uuid}-error` : null"
      :aria-invalid="error ? true : false"
      :class="{ error }"
    />
    <img src="/images/icon-error.svg" class="icon-error" alt="Exclamation point" />
  </div>

  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>
