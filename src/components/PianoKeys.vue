<script setup>
    const props = defineProps(['musicalNotes', 'useKeyboard'])

    // var pianoKeysDiv = document.getElementById('piano-keys');
    // pianoKeysDiv.scrollLeft = (pianoKeysDiv.scrollWidth / 9) * 3;
    
    defineEmits(['checkedChanged', 'notePressed', 'noteReleased'])
</script>

<template>
    <div id="use-keyboard">
        <input 
            type="checkbox" 
            id="use-keyboard" 
            :checked="props.useKeyboard" 
            @change="$emit('checkedChanged', props.useKeyboard)">
        Use Keyboard as Controller - A, S, D, F, G, H, J, K, L, ;
    </div>

    <div id="piano-keys">
        <div 
            v-for="(note, index) in props.musicalNotes" 
            :class="(note.name[1] != 'b') ? 'white-key': 'black-key'" 
            @mousedown="$emit('notePressed', index)" 
            @mouseup="$emit('noteReleased', index)" 
            @touchstart="$emit('notePressed', index)" 
            @touchend="$emit('noteReleased', index)" 
            @touchcancel="$emit('noteReleased', index)"
        >
            <span class="key-label">
                {{ note.name }}
                <!-- - {{ note.frequency }} -->
            </span>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    $screen-sm-min: 0px;
    $screen-sm-max: 1080px;
    $screen-md-min: 1081px;
    $screen-md-max: 1279px;
    $screen-lg-min: 1260px;
    $screen-lg-max: 7000px;

    @mixin bottom-shadow() {
        -moz-box-shadow:    0 2px 4px 2px #000;
        -webkit-box-shadow: 0 2px 4px 2px #000;
        box-shadow:         0 2px 4px 2px #000;
    }

    #piano-keys {
        position: absolute;
        white-space: nowrap;
        width: 100%;
        height: 420px;
        overflow-x: scroll;
        
        @include bottom-shadow();

        .white-key, .black-key {
            position: relative;
            display: inline-block;
            // display: flex;
            width: 36px;
            font-size: 0.7rem;
            text-align: center;
            // bottom: 0.5rem;
        }

        .white-key {
            z-index: 1;
            color: black;
            background-color: white;
            border: solid black;
            border-width: 0 1px 1px 1px;
            height: 100%;
        }
        
        .black-key {
            position: absolute;
            top: 0;
            z-index: 10;
            color: white;
            background-color: black;
            border: solid white;
            border-width: 0 1px 1px 1px;
            height: 60%;
            margin-left: -18px;
            margin-right: -18px;
        }
        
        .key-label {
            position: absolute;
            display: none;
            // align-self: flex-end;
            width: 100%;
            bottom: 0;
            text-align: center;
        }
    }

    /* phone */
    @media screen and (max-width: $screen-sm-max) {
        font, p, input[type=text] {
            font-size: 80px;
        }
        
        input[type=button] {
            margin: 48px;
            width: 400px;
            height: 300px;
        }
        
        input[type=text] {
            width: 260px;
            height: 90px;
        }
        
        #piano-keys {
            .white-key, .black-key {
                position: relative;
                width: 50px;
            }
            .white-key {
                height: 200px;
            }

            .black-key {
                height: 120px;
                margin-left: -25px;
                margin-right: -25px;
            }
        }
    }
</style>