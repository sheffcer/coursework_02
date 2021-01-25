<template>
  <div class="form-control">
    <label for="value">Значение</label>
    <textarea
      :class="{invalid: error}"
      id="value"
      rows="3"
      :placeholder="placeholder"
      :value="modelValue"
      @input="onChange"
      ></textarea>
      <small v-if="error">{{error}}</small>
  </div>
</template>

<script>
export default {
  emits: ['update:modelValue'],
  props: {
    placeholder: String,
    title: String,
    modelValue: String,
    error: String
  },
  methods: {
    onChange (evt) {
      this.$emit('update:modelValue', evt.target.value)
    }
  }
}
</script>

<style lang="css">

</style>
