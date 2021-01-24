<template>
  <div class="form-control">
    <label for="type">Тип блока</label>
    <select id="type" @change="onChange($event)">
      <option
      v-for="option in options"
      :key="option"
      :value="option.value"
      >
        {{ option.tag }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  emits: ['change:selected'],
  props: {
    options: {
      type: Array,
      required: true
    },
    selected: String
  },
  methods: {
    onChange (event) {
      this.$emit('change:selected', event.target.value)
      console.log(event.target.value)
    }
  }
}
</script>

<style lang="css">
</style>
