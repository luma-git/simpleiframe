<template>
    <label v-if="label" :for="uuid" class="mt-4 mb-2">
        {{ label }}
    </label>
    <select class="field form-select mb-2" v-bind="{
      ...$attrs,
      onChange: updateValue
    }" :value="modelValue" :id="uuid">
        <option v-for="option in options" :value="option" :key="option" :selected="option === modelValue">
            {{ option }}
        </option>
    </select>
</template>
  
<script>
import SetupFormComponent from '@/features/SetupFormComponent'
import UniqueID from '@/features/UniqueID'
export default {
    props: {
        options: {
            type: Array,
            required: true
        },
        label: {
            type: String,
            default: ''
        },
        modelValue: {
            type: [String, Number]
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