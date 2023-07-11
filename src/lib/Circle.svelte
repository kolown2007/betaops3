<script lang="ts">
    import { afterUpdate } from "svelte";
    import * as PIXI from "pixi.js";
  
    export let app: PIXI.Application;
    export let x = 0;
    export let y = 0;
    export let radius = 50;
  
    let graphics: PIXI.Graphics;
  
    afterUpdate(() => {
      if (!graphics) {
        graphics = new PIXI.Graphics();
        app.stage.addChild(graphics);
      }
  
      graphics.clear();
      graphics.beginFill(0xff0000);
      graphics.drawCircle(x, y, radius);
      graphics.endFill();
    });
  </script>
  
  