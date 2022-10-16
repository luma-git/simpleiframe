<template>
    <label v-if="label" :for="uuid" class="form-label mt-4">
        {{ label }}
    </label>
    <input class="field form-control mb-2" v-bind="{
      ...$attrs,
      onInput: updateValue
    }" :id="uuid" :value="modelValue" :placeholder="label">
</template>
  
<script>
import SetupFormComponent from '@/features/SetupFormComponent'
import UniqueID from '@/features/UniqueID'
export default {
    props: {
        label: {
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