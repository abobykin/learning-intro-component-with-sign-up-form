<template>
  <p aria-live="assertive" class="form__field__error--message" :class="shown && 'shown'" :id="id">
    <slot />
  </p>
</template>

<script>
export default {
  props: {
    id: {
      type: [String, Number],
      required: true
    },
    shown: {
      type: Boolean,
      required: false
    }
  }
}
</script>
