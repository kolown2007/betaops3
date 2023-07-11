<script lang="ts">

import * as Tone from 'tone'
import{onMount } from 'svelte'
 import { writable, type Writable } from 'svelte/store';
 import * as PIXI from 'pixi.js';
 

export const count = writable(0);


let synth: Tone.Synth;
let meter: Tone.Meter ;
let mic: Tone.UserMedia;
let soundStream:number;
let analyze:Tone.Analyser;
let app: PIXI.Application;




onMount(()=> {

    //pixi canvas

    const canvas = document.getElementById('canvas') as HTMLCanvasElement;
    app = new PIXI.Application({
      view: canvas,
      backgroundAlpha: 0,
      width: window.innerWidth,
      height: window.innerHeight,
       backgroundColor: 0x5fa6ed,
      resizeTo: window,
    });





   //tone.js

    synth = new Tone.Synth().toDestination();
    meter = new Tone.Meter();
    mic = new Tone.UserMedia();
    mic.open();


    analyze = new Tone.Analyser("fft",32);
    mic.connect(analyze);
    mic.connect(meter)

    //setInterval(() => console.log(analyze.getValue()), 10000);




    


    // const numCircles = 1;
    //   for (let i = 0; i < numCircles; i++) {
    //   const circle = new PIXI.Graphics();
    //   circle.beginFill(0x339322);
    //   circle.drawCircle(100, 200 , 50);
    //   circle.endFill();
    
    //   app.stage.addChild(circle);
    // }


const values = meter.getValue();


let value;
if (Array.isArray(values)) {
  value = values[0]; // Use the first value from the array
} else {
  value = values; // Use the single value
}


// Calculate the circle size based on the value
const minSize = 10;
const maxSize = 100;
const circleSize = mapValue(value, 0, 1, minSize, maxSize);


/////


// Create a circle using Pixi.js
const circle = new PIXI.Graphics();
circle.beginFill(0x339322);
circle.drawCircle(0, 0, circleSize);
circle.endFill();
circle.position.set(200, 200);

// Add the circle to the stage and render it
app.stage.addChild(circle);
app.renderer.render(app.stage);

/////

function mapValue(value: number , valueMin: number, valueMax: number, targetMin: number, targetMax: number) {
  const normalizedValue = (value - valueMin) / (valueMax - valueMin);
  return targetMin + (targetMax - targetMin) * normalizedValue;

}


//////

});



            function sound(){     
            synth.triggerAttackRelease("C4", "8n");
            }


            function start(){
            Tone.start();
            console.log('restarted');
            }

            function soundvalue() {
            const soundz = meter.getValue();
            let singleValue;

            if (Array.isArray(soundz)) {
                singleValue = soundz[0];
            } else {
                singleValue = soundz;
            }

            return singleValue;
            }

// const value = soundvalue();
// console.log(value);









</script>



<button on:click={start}>restart</button>
<button on:click={sound}>check</button>

<canvas id="canvas" />

<!-- 
<h1> {soundStream}</h1> -->
