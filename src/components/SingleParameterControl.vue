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
    <fieldset 
        :class="(isVertical) ? 'vertical-range control-column single-parameter-control': 'horizontal-range control-column single-parameter-control'" 
        :id="controlKey">
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

<style lang="scss">
    .single-parameter-control {
        &.horizontal-range {
            padding-bottom: 0;
        }
        &.vertical-range {
            padding-bottom: 8px;
        }
        .horizontal-range {
            width: 90px;
            height: 32px;
        }
        .vertical-range {
            display: block;
            width: 32px;
            height: 90px;
            -webkit-appearance: slider-vertical;
            appearance: slider-vertical;
            writing-mode: bt-lr;
        }
    }
</style>