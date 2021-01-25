<template>
  <div class="avatar">
    <img :src="message" v-bind="$attrs">
  </div>
</template>

<script>
export default {
  props: {
    message: String
  }
}
</script>

<style lang="css">

</style>
