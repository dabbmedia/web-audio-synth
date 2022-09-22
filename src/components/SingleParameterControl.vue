<script setup>
import { ref } from 'vue'

const props = defineProps(['controlKey', 'title', 'controlEnabledCheckId', 'numberInputId', 'rangeInputId', 'defaultValue', 'min', 'max', 'isVertical'])

let controlValue = ref(props.defaultValue)

const emit = defineEmits(['controlValueChanged', 'checkEnabledChanged'])

let updateValue = (event) => {
    controlValue.value = event.target.value
    emit('controlValueChanged', event.target.parentNode.id, event.target.value)
}
let updateChecked = (event) => {
    emit('checkEnabledChanged', event.target.parentNode.parentNode.id, event.target.checked)
}
</script>

<template>
    <fieldset class="control-column" :id="controlKey">
        <legend><input v-if="controlEnabledCheckId" type="checkbox" :id="controlEnabledCheckId" @change="updateChecked">{{ title }}</legend>
            
        <input 
            type="number" 
            :id="numberInputId" 
            :min="min" 
            :max="max" 
            :value="controlValue" 
            @change="updateValue">
        
        <input 
            type="range" 
            :id="rangeInputId" 
            :min="min" 
            :max="max" 
            step="0.1" 
            :class="(isVertical) ? 'vertical-range': 'horizontal-range'" 
            :orient="(isVertical) ? 'vertical': 'horizontal'" 
            :value="controlValue" 
            @input="updateValue">
    </fieldset>
</template>
