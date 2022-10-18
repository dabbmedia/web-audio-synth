<script setup>
const props = defineProps(['controlKey', 'controlData'])

const emit = defineEmits(['controlValueChanged', 'checkEnabledChanged', 'increaseValue', 'decreaseValue'])
</script>

<template>
    <fieldset 
        :class="(props.controlData.isVertical) ? 'vertical-range control-column single-parameter-control': 'horizontal-range control-column single-parameter-control'" 
        :id="props.controlKey">
        <legend>
            <input 
                v-if="props.controlData.controlEnabledCheckId" 
                type="checkbox" 
                :id="props.controlData.controlEnabledCheckId" 
                @change="$emit('checkEnabledChanged', props.controlKey, $event.target.checked)">{{ props.controlData.title }}
            </legend>
            
        <div class="value-container">
            <input 
                type="text" 
                :id="props.controlData.numberInputId" 
                :min="props.controlData.min" 
                :max="props.controlData.max"  
                :value="props.controlData.currentValue" 
                @change="$emit('controlValueChanged', props.controlKey, $event.target.value)">
            
            <div class="increase-decrease-container">
                <button class="control-value-increase" @click="$emit('increaseValue', props.controlKey)">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-caret-up-fill" viewBox="0 0 16 16"><path d="m7.247 4.86-4.796 5.481c-.566.647-.106 1.659.753 1.659h9.592a1 1 0 0 0 .753-1.659l-4.796-5.48a1 1 0 0 0-1.506 0z"/></svg>
                </button>
                <button class="control-value-decrease" @click="$emit('decreaseValue', props.controlKey)">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-caret-down-fill" viewBox="0 0 16 16"><path d="M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z"/></svg>
                </button>
            </div>
        </div>
        
        <input 
            type="range" 
            :id="props.controlData.rangeInputId" 
            :min="props.controlData.min" 
            :max="props.controlData.max"  
            :step="props.controlData.step" 
            :orient="(props.controlData.isVertical) ? 'vertical': 'horizontal'" 
            :value="props.controlData.currentValue" 
            @input="$emit('controlValueChanged', props.controlKey, $event.target.value)">
    </fieldset>
</template>

<style lang="scss">
    .single-parameter-control {
        .value-container {
            display: flex;
            flex-direction: row;
            // align-items: center;

            input[type=text] {
                z-index: 1;
                width: 3rem;
                height: 1.55rem;
                font-size: 0.8rem;
                text-align: right;
                border: 1px solid black;
                border-radius: 0.15rem;
                padding-right: 0.87rem;
            }
            .increase-decrease-container {
                display: flex;
                z-index: 2;
                flex-direction: column;
                margin-top: 0.25rem;
                margin-left: -0.86rem;
                
                .control-value-increase, .control-value-decrease {
                    -webkit-appearance: none;
                    -moz-appearance: none;
                    appearance: none;
                    width: 12px;
                    height: 0.5rem;
                    padding: 0;
                    margin: 0;
                    background: none;
                    border: none;
                    border-radius: 0.125rem;
                    text-align: center;

                    svg {
                        position: absolute;
                        top: 0.015rem;
                        left: 0.09rem;
                        margin: 0;
                        padding: 0;
                        width: 8px;
                        height: 8px;
                    }
                }
            }
        }
        &.horizontal-range {
            padding-bottom: 0;

            input[type=range] {
                width: 90px;
                height: 32px;
            }
        }
        &.vertical-range {
            padding-bottom: 8px;

            input[type=range] {
                width: 32px;
                height: 90px;
                -webkit-appearance: slider-vertical;
                appearance: slider-vertical;
                writing-mode: bt-lr;
            }
        }
    }
</style>