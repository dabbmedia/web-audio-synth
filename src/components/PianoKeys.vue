<script setup>
    import { ref, onMounted } from 'vue'
    const props = defineProps(['musicalNotes', 'useKeyboard'])

    let pianoKeysDiv
    
    const emit = defineEmits(['checkedChanged', 'notePressed', 'noteReleased'])

    onMounted(() => {
        pianoKeysDiv = document.getElementById('piano-keys')
        pianoKeysDiv.scrollLeft = (pianoKeysDiv.scrollWidth / 9) * 3
    })

    const emitPressed = (e, index) => {
        console.log('piano key pressed');
        e.preventDefault();
        emit('notePressed', index);
        e.target.classList.add('note-pressed');
    }

    const emitReleased = (e, index) => {
        console.log('piano key released');
        e.preventDefault();
        emit('noteReleased', index);
        e.target.classList.remove('note-pressed');
    }
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
        <!-- 
            these events caused a double note press,
            but may be needed for "sliding" off of a piano key
            @mouseout="emitReleased($event, index)" 
            @mouseleave="emitReleased($event, index)" 
        -->
        <div 
            v-for="(note, index) in props.musicalNotes" 
            :class="(note.name[1] != 'b') ? 'white-key': 'black-key'" 
            @mousedown="emitPressed($event, index)" 
            @mouseup="emitReleased($event, index)"  
            @touchstart="emitPressed($event, index)" 
            @touchend="emitReleased($event, index)" 
            @touchcancel="emitReleased($event, index)" 
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