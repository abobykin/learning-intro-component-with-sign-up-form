<template>
  <p aria-live="assertive" class="form__field__error--message" :id="id">
    <slot />
  </p>
</template>

<script>
export default {
  props: {
    id: {
      type: [String, Number],
      required: true
    }
  }
}
</script>
