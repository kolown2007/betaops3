<script lang="ts">
  import { onMount } from "svelte";
  import * as PIXI from "pixi.js";
  import Hello from "$lib/Circle.svelte"

  let app: PIXI.Application;

  onMount(() => {
    const canvas = document.getElementById("canvas") as HTMLCanvasElement;

    app = new PIXI.Application({
      antialias: true,
      view: canvas,
      // backgroundAlpha: 0,
      width: window.innerWidth,
      height: window.innerHeight,
      backgroundColor: 0x5fa6ed,
      resizeTo: window,
    });

    const numCircles = 10;
    const circles: PIXI.Graphics[] = [];
    let round:PIXI.Graphics;

    for (let i = 0; i < numCircles; i++) {
      const circle = new PIXI.Graphics();
      circle.beginFill(getRandomColor());
      circle.drawCircle(getRandomY(),getRandomY(), 50);
      circle.endFill();
     

    //app.stage.addChild(circle);

      circles.push(circle);
    }

    //round
     round= new PIXI.Graphics();
     round.beginFill(getRandomColor());
     round.drawCircle(0,0,100);
    
     round.position.x = 300;
     round.position.y = 300;
     round.interactive = true;


     round.on('pointerdown', onClick);

     function onClick()
     {
    round.scale.x *= 1.25;
    round.scale.y *= 1.25;
     }

    
    //app.stage.addChild(round)


    //square
    const graphics = new PIXI.Graphics();
    graphics.beginFill(0xde3249);
    graphics.drawRect(300, 200, 100, 100);
    graphics.endFill();

    graphics.pivot.x = 50;
    graphics.pivot.y = 50;

    //app.stage.addChild(graphics);

    //animation
    app.ticker.add(() => {
      graphics.rotation += 0.001;
      round.position.x += 0.5;
    
   
    });
  });

  function getRandomX() {
    return Math.random() * window.innerWidth;
  }

  function getRandomY() {
    return Math.random() * window.innerHeight;
  }

  function getRandomColor() {
    return Math.random() * 0xffffff;
  }




</script>




<head>
  <title>Beta_Ops_3</title>
</head>

<Hello app={app} x={400} y={300} radius={50} />
<canvas id="canvas" /> 



<style>
  #canvas {
    overflow: hidden;
    position: fixed;
    top: 0;
    left: 0;
  }
</style>
