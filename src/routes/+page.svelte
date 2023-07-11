<script lang="ts">
    import { onMount } from 'svelte';
    import * as PIXI from 'pixi.js';
  

    let app: PIXI.Application;
    let circle: PIXI.Graphics;
   

    onMount(() => {
      // Create the Pixi.js application and renderer
      const canvas = document.getElementById('canvas') as HTMLCanvasElement;
      app = new PIXI.Application({
        view: canvas,
        // backgroundAlpha: 0,
        width: window.innerWidth,
        height: window.innerHeight,
       
        // backgroundColor: 0x5fa6ed,
        resizeTo: window ,
       
      });


      const numCircles = 10000;
      for (let i = 0; i < numCircles; i++) {
      const circle = new PIXI.Graphics();
      circle.beginFill(getRandomColor());
      circle.drawCircle(0, 0, 50);
      circle.endFill();
      circle.position.set(getRandomX(), getRandomY());

      app.stage.addChild(circle);
    }




  



    function getRandomX() {
    return Math.random() * window.innerWidth;
    }

    function getRandomY() {
    return Math.random() * window.innerHeight;
    }

    function getRandomColor() {
    return Math.random() * 0xffffff;
  }
    });





  </script>

  <head>

  <title>Beta_Ops_3</title>
  </head>
  
  <canvas id="canvas" />


  <style>
  
    
    #canvas {
      overflow: hidden;
      position: fixed;
      top: 0;
      left: 0;
    }
  </style>
  