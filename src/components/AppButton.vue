<template>
    <p>
      <!-- <button class="btn primary">Загрузить комментарии</button> -->
      <button class="btn" :class="color" @click="$emit('action')">
      <slot/>
    </button>
    </p>
</template>

<script>
export default {
  props: {
    // text: {
    //   type: String,
    //   required: true
    // },
    color: {
      type: String,
      default: '',
      validator (value) {
        return ['', 'primary', 'danger'].includes(value)
      }
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
