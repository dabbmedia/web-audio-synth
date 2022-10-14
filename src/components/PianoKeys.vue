<script setup>
    import { ref, onMounted } from 'vue'
    const props = defineProps(['musicalNotes', 'useKeyboard'])

    let pianoKeysDiv
    
    defineEmits(['checkedChanged', 'notePressed', 'noteReleased'])

    onMounted(() => {
        pianoKeysDiv = document.getElementById('piano-keys')
        pianoKeysDiv.scrollLeft = (pianoKeysDiv.scrollWidth / 9) * 3
    })
</script>

<template>
    <div id="use-keyboard">
        <input 
            type="checkbox" 
            id="use-keyboard" 
            :checked="props.useKeyboard" 
            @change="$emit('checkedChanged', props.useKeyboard)">
        Use Keyboard as Controller
    </div>
    <div>(A, S, D, F, G, H, J, K, L, ;)</div>

    <div id="piano-keys">
        <div 
            v-for="(note, index) in props.musicalNotes" 
            :class="(note.name[1] != 'b') ? 'white-key': 'black-key'" 
            @mousedown="$emit('notePressed', index); $event.preventDefault(); $event.target.classList.add('note-pressed');" 
            @mouseup="$emit('noteReleased', index); $event.preventDefault(); $event.target.classList.remove('note-pressed');" 
            @mouseleave="$emit('noteReleased', index); $event.preventDefault(); $event.target.classList.remove('note-pressed');" 
            @mouseout="$emit('noteReleased', index); $event.preventDefault(); $event.target.classList.remove('note-pressed');" 
            @touchstart="$emit('notePressed', index); $event.preventDefault(); $event.target.classList.add('note-pressed');" 
            @touchend="$emit('noteReleased', index); $event.preventDefault(); $event.target.classList.remove('note-pressed');" 
            @touchcancel="$emit('noteReleased', index); $event.preventDefault(); $event.target.classList.remove('note-pressed');"
        >
            <span class="key-label">{{ note.name }}</span>
        </div>
    </div>
</template>

<style lang="scss" scoped>
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
        .note-pressed {
            box-shadow: inset 2rem 1rem rgba(128, 128, 128, 0.7);
            // background-color: red;
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

    select {
        appearance: none;
        background: none;
    }

    /* phone */
    // @media screen and (max-width: var(--screen-sm-max)) {
    //     font, p, input[type=text] {
    //         font-size: 80px;
    //     }
        
    //     input[type=button] {
    //         margin: 48px;
    //         width: 400px;
    //         height: 300px;
    //     }
        
    //     input[type=text] {
    //         width: 260px;
    //         height: 90px;
    //     }
        
    //     #piano-keys {
    //         .white-key, .black-key {
    //             position: relative;
    //             display: block;
    //             height: 50px;
    //         }
    //         .white-key {
    //             width: 100%;
    //         }

    //         .black-key {
    //             width: 60%;
    //             margin: -25px 0;
    //         }
    //     }
    // }
</style>