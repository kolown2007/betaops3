<script lang="ts">
    import { onMount } from "svelte";
    import * as PIXI from "pixi.js";
    import Circle from "$lib/Circle.svelte";
  
    let app: PIXI.Application;
  
    onMount(() => {
      const canvas = document.getElementById("canvas") as HTMLCanvasElement;
  
      app = new PIXI.Application({
        antialias: true,
        view: canvas,
        width: window.innerWidth,
        height: window.innerHeight,
        backgroundColor: 0x5fa6ed,
        resizeTo: window,
      });
    });
  </script>
  
  <!-- <canvas id="canvas" /> -->
  <Circle app={app} x={400} y={300} radius={50} />
  