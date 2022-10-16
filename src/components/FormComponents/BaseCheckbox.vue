<template>
  <div class="form-check mt-4">
    <input class="form-check-input" type="checkbox" :checked="modelValue"
      @change="$emit('update:modelValue', $event.target.checked)">
    <label v-if="label" class="form-check-label">
      {{ label }}
    </label>
  </div>
</template>
  
<script>
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: Boolean,
      default: false
    }
  }
}
</script>