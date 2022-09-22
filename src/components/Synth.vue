<script setup>
    import '../assets/style.scss'
    import { ref } from 'vue'
    import { reactive } from 'vue'
    import SingleParameterControl from './SingleParameterControl.vue'
    import PianoKeys from './PianoKeys.vue'

    const nodeControls = reactive({
        masterGain: {title: 'Volume', numberInputId: 'master-gain-value', rangeInputId: 'master-gain-range', currentValue: '0.8', audioNode: '', min: '0.0', max: '1.0', parameter: 'gain', enabled: true, isVertical: true},
        // distortion: {title: 'Distortion', controlEnabledCheckId: 'send-effect-distortion-check', numberInputId: 'distortion-value', rangeInputId: 'distortion-range', currentValue: '0.8', audioNode: '', min: '0.0', max: '1.0', parameter: 'gain', enabled: false, isVertical: true},
        delay: {title: 'Delay', controlEnabledCheckId: 'send-effect-delay-check', numberInputId: 'delay-value', rangeInputId: 'delay-range', currentValue: '2.0', audioNode: '', min: '0.0', max: '6.0', parameter: 'delayTime', enabled: false, isVertical: true},
        // reverb: {title: 'Reverb', controlEnabledCheckId: 'send-effect-reverb-check', numberInputId: 'reverb-value', rangeInputId: 'reverb-range', currentValue: '0.8', audioNode: '', min: '0.0', max: '1.0', parameter: 'gain', enabled: true, isVertical: true},
        eqLow: {title: 'EQ Low', numberInputId: 'eq-low-value', rangeInputId: 'eq-low-range', currentValue: '0.5', audioNode: '', min: '0.0', max: '1.0', parameter: 'gain', enabled: true, isVertical: true},
        eqMid: {title: 'EQ Mid', numberInputId: 'eq-mid-value', rangeInputId: 'eq-mid-range', currentValue: '0.5', audioNode: '', min: '0.0', max: '1.0', parameter: 'gain', enabled: true, isVertical: true},
        eqHigh: {title: 'EQ High', numberInputId: 'eq-high-value', rangeInputId: 'eq-high-range', currentValue: '0.5', audioNode: '', min: '0.0', max: '1.0', parameter: 'gain', enabled: true, isVertical: true},
        compressor: {title: 'Compressor', numberInputId: 'eq-compressor-value', rangeInputId: 'eq-compressor-range', currentValue: '3', audioNode: '', min: '1', max: '20', parameter: 'ratio', enabled: true, isVertical: false},
        pan: {title: 'Pan', numberInputId: 'eq-pan-value', rangeInputId: 'eq-pan-range', currentValue: '0.0', audioNode: '', min: '-1.0', max: '1.0', parameter: 'pan', enabled: true, isVertical: false},
    })

    const pianoKeys = ref({
        useKeyboard: false
    })

    const musicalNotes = [
        {name: 'C0', frequency: 16.35},
        {name: 'Db0', frequency: 17.32},
        {name: 'D0', frequency: 18.35},
        {name: 'Eb0', frequency: 19.45},
        {name: 'E0', frequency: 20.6},
        {name: 'F0', frequency: 21.83},
        {name: 'Gb0', frequency: 23.12},
        {name: 'G0', frequency: 24.5},
        {name: 'Ab0', frequency: 25.96},
        {name: 'A0', frequency: 27.5},
        {name: 'Bb0', frequency: 29.14},
        {name: 'B0', frequency: 30.87},
        {name: 'C1', frequency: 32.7},
        {name: 'Db1', frequency: 34.65},
        {name: 'D1', frequency: 36.71},
        {name: 'Eb1', frequency: 38.89},
        {name: 'E1', frequency: 41.2},
        {name: 'F1', frequency: 43.65},
        {name: 'Gb1', frequency: 46.25},
        {name: 'G1', frequency: 49},
        {name: 'Ab1', frequency: 51.91},
        {name: 'A1', frequency: 55},
        {name: 'Bb1', frequency: 58.27},
        {name: 'B1', frequency: 61.74},
        {name: 'C2', frequency: 65.41},
        {name: 'Db2', frequency: 69.3},
        {name: 'D2', frequency: 73.42},
        {name: 'Eb2', frequency: 77.78},
        {name: 'E2', frequency: 82.41},
        {name: 'F2', frequency: 87.31},
        {name: 'Gb2', frequency: 92.5},
        {name: 'G2', frequency: 98},
        {name: 'Ab2', frequency: 103.83},
        {name: 'A2', frequency: 110},
        {name: 'Bb2', frequency: 116.54},
        {name: 'B2', frequency: 123.47},
        {name: 'C3', frequency: 130.81},
        {name: 'Db3', frequency: 138.59},
        {name: 'D3', frequency: 146.83},
        {name: 'Eb3', frequency: 155.56},
        {name: 'E3', frequency: 164.81},
        {name: 'F3', frequency: 174.61},
        {name: 'Gb3', frequency: 185},
        {name: 'G3', frequency: 196},
        {name: 'Ab3', frequency: 207.65},
        {name: 'A3', frequency: 220},
        {name: 'Bb3', frequency: 233.08},
        {name: 'B3', frequency: 246.94},
        {name: 'C4', frequency: 261.63},
        {name: 'Db4', frequency: 277.18},
        {name: 'D4', frequency: 293.66},
        {name: 'Eb4', frequency: 311.13},
        {name: 'E4', frequency: 329.63},
        {name: 'F4', frequency: 349.23},
        {name: 'Gb4', frequency: 369.99},
        {name: 'G4', frequency: 392},
        {name: 'Ab4', frequency: 415.3},
        {name: 'A4', frequency: 440},
        {name: 'Bb4', frequency: 466.16},
        {name: 'B4', frequency: 493.88},
        {name: 'C5', frequency: 523.25},
        {name: 'Db5', frequency: 554.37},
        {name: 'D5', frequency: 587.33},
        {name: 'Eb5', frequency: 622.25},
        {name: 'E5', frequency: 659.25},
        {name: 'F5', frequency: 698.46},
        {name: 'Gb5', frequency: 739.99},
        {name: 'G5', frequency: 783.99},
        {name: 'Ab5', frequency: 830.61},
        {name: 'A5', frequency: 880},
        {name: 'Bb5', frequency: 932.33},
        {name: 'B5', frequency: 987.77},
        {name: 'C6', frequency: 1046.5},
        {name: 'Db6', frequency: 1108.73},
        {name: 'D6', frequency: 1174.66},
        {name: 'Eb6', frequency: 1244.51},
        {name: 'E6', frequency: 1318.51},
        {name: 'F6', frequency: 1396.91},
        {name: 'Gb6', frequency: 1479.98},
        {name: 'G6', frequency: 1567.98},
        {name: 'Ab6', frequency: 1661.22},
        {name: 'A6', frequency: 1760},
        {name: 'Bb6', frequency: 1864.66},
        {name: 'B6', frequency: 1975.53},
        {name: 'C7', frequency: 2093},
        {name: 'Db7', frequency: 2217.46},
        {name: 'D7', frequency: 2349.32},
        {name: 'Eb7', frequency: 2489.02},
        {name: 'E7', frequency: 2637.02},
        {name: 'F7', frequency: 2793.83},
        {name: 'Gb7', frequency: 2959.96},
        {name: 'G7', frequency: 3135.96},
        {name: 'Ab7', frequency: 3322.44},
        {name: 'A7', frequency: 3520},
        {name: 'Bb7', frequency: 3729.31},
        {name: 'B7', frequency: 3951.07},
        {name: 'C8', frequency: 4186.01},
        {name: 'Db8', frequency: 4434.92},
        {name: 'D8', frequency: 4698.63},
        {name: 'Eb8', frequency: 4978.03},
        {name: 'E8', frequency: 5274.04},
        {name: 'F8', frequency: 5587.65},
        {name: 'Gb8', frequency: 5919.91},
        {name: 'G8', frequency: 6271.93},
        {name: 'Ab8', frequency: 6644.88},
        {name: 'A8', frequency: 7040},
        {name: 'Bb8', frequency: 7458.62},
        {name: 'B8', frequency: 7902.13},
    ]

    let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    let gainMaster = audioCtx.createGain();
    gainMaster.gain.value = parseFloat(nodeControls.masterGain.currentValue);
    
    nodeControls.masterGain.audioNode = audioCtx.createGain();
    nodeControls.masterGain.audioNode.gain.value = parseFloat(nodeControls.masterGain.currentValue);

    nodeControls.eqLow.audioNode = audioCtx.createBiquadFilter();
    nodeControls.eqLow.audioNode.type = 'lowshelf';
    nodeControls.eqLow.audioNode.frequency.value = 300;
    nodeControls.eqLow.audioNode.gain.value = 0;
    
    let destinationMaster = audioCtx.destination;
    let oscillatorType = 0;
    let oscillators = [];
    let midi = null;
    let sustainPedalPressed = false;

    let createSendChain = function() {
        // distortion
        // oscSend = audioCtx.createWaveShaper();
        // oscSend.curve = makeDistortionCurve(80); //0-100 optimal
        // oscSend.oversample = "4x";

        // reverb
        // oscSend = audioCtx.createConvolver();

        // delay
        if (nodeControls.delay.enabled && !nodeControls.delay.audioNode) {
            nodeControls.delay.audioNode = audioCtx.createDelay(nodeControls.delay.max);
            nodeControls.delay.audioNode.delayTime.setValueAtTime(nodeControls.delay.currentValue, audioCtx.currentTime);
            
            const delayGainNode = audioCtx.createGain();
            delayGainNode.gain.value = 0.1;

            nodeControls.masterGain.audioNode.connect(delayGainNode);
            delayGainNode.connect(nodeControls.delay.audioNode);

            nodeControls.delay.audioNode.connect(nodeControls.eqLow.audioNode);
        } else if (nodeControls.delay.audioNode && !nodeControls.delay.enabled) {
            nodeControls.delay.audioNode.disconnect();
            nodeControls.masterGain.audioNode.connect(nodeControls.eqLow.audioNode);
        } else {
            nodeControls.masterGain.audioNode.connect(nodeControls.eqLow.audioNode);
        }
    }
    let createMasterChain = function() {
        nodeControls.pan.audioNode = audioCtx.createStereoPanner();
        nodeControls.pan.audioNode.pan.setValueAtTime(0, audioCtx.currentTime);
        
        nodeControls.eqMid.audioNode = audioCtx.createBiquadFilter();
        nodeControls.eqMid.audioNode.type = 'peaking';
        nodeControls.eqMid.audioNode.frequency.value = 440;
        nodeControls.eqMid.audioNode.Q.value = 0; //larger value means smaller band
        nodeControls.eqMid.audioNode.gain.value = 0;
        
        nodeControls.eqHigh.audioNode = audioCtx.createBiquadFilter();
        nodeControls.eqHigh.audioNode.type = 'highshelf';
        nodeControls.eqHigh.audioNode.frequency.value = 1000;
        nodeControls.eqHigh.audioNode.gain.value = 0;

        nodeControls.compressor.audioNode = audioCtx.createDynamicsCompressor();
        nodeControls.compressor.audioNode.threshold.setValueAtTime(-50, audioCtx.currentTime);
        nodeControls.compressor.audioNode.knee.setValueAtTime(40, audioCtx.currentTime);
        nodeControls.compressor.audioNode.ratio.setValueAtTime(nodeControls.compressor.currentValue, audioCtx.currentTime);
        nodeControls.compressor.audioNode.attack.setValueAtTime(0, audioCtx.currentTime);
        nodeControls.compressor.audioNode.release.setValueAtTime(0.25, audioCtx.currentTime);
        
        nodeControls.eqLow.audioNode.connect(nodeControls.eqMid.audioNode);
        nodeControls.eqMid.audioNode.connect(nodeControls.eqHigh.audioNode);
        nodeControls.eqHigh.audioNode.connect(nodeControls.compressor.audioNode);
        nodeControls.compressor.audioNode.connect(nodeControls.pan.audioNode);
        
        nodeControls.pan.audioNode.connect(destinationMaster);
    }
    let checkEnabledChanged = function(controlName, isChecked) {
        nodeControls[controlName].enabled = isChecked;
        createSendChain();
    }
    let controlValueChanged = function(controlName, newValue) {
        let control = nodeControls[controlName];
        if (control) {
            control.currentValue = newValue;
            if (control.audioNode[control.parameter]) {
                control.currentValue = newValue;
                control.audioNode[control.parameter].setValueAtTime(newValue, audioCtx.currentTime);
            }
        } else {
            console.log(`Control ${controlName} not found, value could not be updated.`);
            return true;
        }
    }
    let createFrequencyOscillator = function(noteNum, start) {
        var oscillator = audioCtx.createOscillator();
        var note = musicalNotes[noteNum];

        oscillatorType = document.getElementById('osc-type').options[document.getElementById('osc-type').selectedIndex].value;
        oscillator.type = oscillatorType;

        // use for custom oscillator wave types
        // const real = new Float32Array(2);
        // const imag = new Float32Array(2);
        
        // real[0] = 0;
        // imag[0] = 0;
        // real[1] = 1;
        // imag[1] = 0;
        
        // const wave = audioCtx.createPeriodicWave(real, imag, {disableNormalization: true});
        // oscillator.setPeriodicWave(wave);

        oscillator.frequency.value = parseFloat(note.frequency); // value in hertz
        
        var gainNode = audioCtx.createGain();
        gainNode.gain.value = nodeControls.masterGain.currentValue;

        oscillator.connect(gainNode).connect(nodeControls.masterGain.audioNode);

        oscillators[noteNum] = [oscillator, gainNode];
    }
    let noteStart = function(noteNum, start) {
        var note = musicalNotes[noteNum];
        
        createFrequencyOscillator(noteNum, start);

        oscillators[noteNum][0].start(start);
        // console.log('osc started: ' + noteNum);
        // printAudioCtx(false);
        oscillators[noteNum][0].onended = function() {
            if (oscillators[noteNum]) {
                oscillators[noteNum][1].disconnect();
                delete oscillators[noteNum];
            }
        };
    }
    let noteStop = function(noteNum) {
        if (oscillators[noteNum]) {
            var eventTime = audioCtx.currentTime;
            var stopTime = eventTime + 0.5;
            oscillators[noteNum][1].gain.setValueAtTime(nodeControls.masterGain.currentValue, eventTime);
            oscillators[noteNum][1].gain.exponentialRampToValueAtTime(0.0001, stopTime);
            oscillators[noteNum][0].stop(stopTime + 0.6);
        }
    }
    let onMIDISuccess = function(midiAccess) {
        midi = midiAccess;  // store in the global (in real usage, would probably keep in an object instance)
        Array.from(midi.inputs).forEach((input) => {
            input[1].onmidimessage = MIDIMessageEventHandler;
        })
    }
    let MIDIMessageEventHandler = function(event) {
        var noteNumber = event.data[1];
        if (event.data[0] == 144) {
            if (event.data[2] > 0) {
                noteStart(noteNumber, 0.001);
            } else if (event.data[2] === 0) {
                if (!sustainPedalPressed) {
                    noteStop(noteNumber);
                }
            }
        } else if (event.data[0] == 176 && event.data[1] == 64) {
            if (event.data[2] === 0) {
                if (sustainPedalPressed) {
                    oscillators.forEach((osc, index) => {
                        if (osc.length === 2) {
                            noteStop(oscillators.indexOf(osc));
                        }
                    });
                }
                sustainPedalPressed = false;
            } else {
                sustainPedalPressed = true;
            }
        }
    }
    let onMIDIFailure = function(msg) {
        console.error(`Failed to get MIDI access - ${msg}`);
    }
    let printAudioCtx = function(allFields) {
        if (!allFields) {
            console.log('baseLatency; ' + audioCtx.baseLatency);
            console.log('outputLatency; ' + audioCtx.outputLatency);
        } else {
            for (let key in audioCtx) {
                console.log('audioCtx key: ' + key + ', value: ' + JSON.stringify(audioCtx[key]));
            }
        }
    }
    let makeDistortionCurve = function(amount) {
        var k = typeof amount === 'number' ? amount : 50,
            n_samples = 44100,
            curve = new Float32Array(n_samples),
            deg = Math.PI / 180,
            i = 0,
            x;
        for ( ; i < n_samples; ++i ) {
            x = i * 2 / n_samples - 1;
            curve[i] = ( 3 + k ) * x * 20 * deg / ( Math.PI + k * Math.abs(x) );
        }
        return curve;
    }
    let keyDownEvent = function(e) {
        switch (e.keyCode) {
            case 'A'.charCodeAt(0):
                noteStart(57);
                break;
            case 'S'.charCodeAt(0):
                noteStart(59);
                break;
            case 'D'.charCodeAt(0):
                noteStart(61);
                break;
            case 'F'.charCodeAt(0):
                noteStart(62);
                break;
            case 'J'.charCodeAt(0):
                noteStart(64);
                break;
            case 'K'.charCodeAt(0):
                noteStart(66);
                break;
            case 'L'.charCodeAt(0):
                noteStart(68);
                break;
            case ';'.charCodeAt(0):
                noteStart(69);
                break;
            case 'Q'.charCodeAt(0):
                noteStart(62);
                break;
            case 'W'.charCodeAt(0):
                noteStart(64);
                break;
            case 'E'.charCodeAt(0):
                noteStart(66);
                break;
            case 'R'.charCodeAt(0):
                noteStart(67);
                break;
            case 'U'.charCodeAt(0):
                noteStart(69);
                break;
            case 'I'.charCodeAt(0):
                noteStart(71);
                break;
            case 'O'.charCodeAt(0):
                noteStart(73);
                break;
            case 'P'.charCodeAt(0):
                noteStart(74);
                break;
        }
    }
    let keyUpEvent = function(e) {
        switch (e.keyCode) {
            case 'A'.charCodeAt(0):
                noteStop(57);
                break;
            case 'S'.charCodeAt(0):
                noteStop(59);
                break;
            case 'D'.charCodeAt(0):
                noteStop(61);
                break;
            case 'F'.charCodeAt(0):
                noteStop(62);
                break;
            case 'J'.charCodeAt(0):
                noteStop(64);
                break;
            case 'K'.charCodeAt(0):
                noteStop(66);
                break;
            case 'L'.charCodeAt(0):
                noteStop(68);
                break;
            case ';'.charCodeAt(0):
                noteStop(69);
                break;
            case 'Q'.charCodeAt(0):
                noteStop(62);
                break;
            case 'W'.charCodeAt(0):
                noteStop(64);
                break;
            case 'E'.charCodeAt(0):
                noteStop(66);
                break;
            case 'R'.charCodeAt(0):
                noteStop(67);
                break;
            case 'U'.charCodeAt(0):
                noteStop(69);
                break;
            case 'I'.charCodeAt(0):
                noteStop(71);
                break;
            case 'O'.charCodeAt(0):
                noteStop(73);
                break;
            case 'P'.charCodeAt(0):
                noteStop(74);
                break;
        }
    }
    let updateKeyEvents = function() {
        if (pianoKeys.useKeyboard) {
            if (window.attachEvent) {
                window.attachEvent("onkeydown", keyDownEvent);
            } else if (window.addEventListener) {
                window.addEventListener("keydown", keyDownEvent);
            }

            if (window.attachEvent) {
                window.attachEvent("onkeyup", keyUpEvent);
            } else if (window.addEventListener) {
                window.addEventListener("keyup", keyUpEvent);
            }
        } else {
            if (window.detachEvent) {
                window.detachEvent("onkeydown", keyDownEvent);
            } else if (window.removeEventListener) {
                window.removeEventListener("keydown", keyDownEvent);
            }

            if (window.detachEvent) {
                window.detachEvent("onkeyup", keyUpEvent);
            } else if (window.removeEventListener) {
                window.removeEventListener("keyup", keyUpEvent);
            }
        }
    }
    let useKeyboardCheckboxChanged = function(isChecked) {
        pianoKeys.useKeyboard = (isChecked) ? false: true;
        updateKeyEvents();
    }
    let toggleControls = function() {
        let toggleControl = document.getElementById('controls-container');
        if (toggleControl.style.display === 'none') {
            document.getElementById('toggle-controls').innerHTML = '<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-caret-down-fill" viewBox="0 0 16 16"><path d="M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z"/></svg>';
            toggleControl.style.display = 'flex'
        } else {
            document.getElementById('toggle-controls').innerHTML = '<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-caret-right-fill" viewBox="0 0 16 16"><path d="m12.14 8.753-5.482 4.796c-.646.566-1.658.106-1.658-.753V3.204a1 1 0 0 1 1.659-.753l5.48 4.796a1 1 0 0 1 0 1.506z"/></svg>';
            toggleControl.style.display = 'none';
        }
    }
    
    createSendChain();
    createMasterChain();

    if (typeof navigator.requestMIDIAccess !== "undefined") {
        navigator.requestMIDIAccess().then(onMIDISuccess, onMIDIFailure)
    } else {
        console.log('MIDI not available');
    }
</script>

<template>
    <h2 id="controls-header">
        Effects
        <span id="toggle-controls" @click="toggleControls">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-caret-down-fill" viewBox="0 0 16 16"><path d="M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z"/></svg>
        </span>
    </h2>
    <div id="controls-container">
        <fieldset class="control-column">
            <legend>Wave Type</legend>
            <select id="osc-type">
                <option value="sine" selected>sine</option>
                <option value="square">square</option>
                <option value="sawtooth">sawtooth</option>
                <option value="triangle">triangle</option>
                <option value="custom">custom</option>
            </select>
        </fieldset>

        <SingleParameterControl 
            v-for="(control, key) in nodeControls" 
            :control-key="key"
            :title="control.title" 
            :controlEnabledCheckId="control.controlEnabledCheckId" 
            :numberInputId="control.numberInputId" 
            :rangeInputId="control.rangeInputId" 
            :defaultValue="control.currentValue" 
            :value="control.value" 
            :min="control.min" 
            :max="control.max" 
            :isVertical="control.isVertical" 
            @control-value-changed="controlValueChanged" 
            @check-enabled-changed="checkEnabledChanged" 
        />
    </div>
    
    <PianoKeys 
        :musical-notes="musicalNotes" 
        :use-keyboard="pianoKeys.useKeyboard" 
        @checked-changed="useKeyboardCheckboxChanged" 
        @note-pressed="noteStart" 
        @note-released="noteStop" 
    />
</template>

<style lang="scss">
    #controls-container {
        display: flex;
        
        .control-column {
            display: inline-block;
            margin: 8px;
            text-align: center;
            border: 0;
        }
        .control-column legend {
            text-align: center;
            margin: 0 auto;
            white-space: nowrap;
        }
        .control-column input[type=checkbox] {
            margin: 0 4px;
        }
        .control-column input[type=number] {
            display: block;
            width: 72px;
            margin: 8px auto;
        }
        .control-column input[type=range] {
            display: block;
            margin: 8px auto;
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