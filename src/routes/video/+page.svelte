<script lang="ts">

    import { onMount } from 'svelte';
    import * as PIXI from 'pixi.js';

   

    let app: PIXI.Application;

    onMount(() => {
      // Create the Pixi.js application and renderer
      const canvas = document.getElementById('canvas') as HTMLCanvasElement;
      app = new PIXI.Application({
        view: canvas,
        // backgroundAlpha: 0,
        width: window.innerWidth,
        height: window.innerHeight,
       
         backgroundColor: 0x5fa6ed,
        resizeTo: window ,
       
      });

      const button = new PIXI.Graphics()
    .beginFill(0x0, 0.5)
    .drawRoundedRect(0, 0, 100, 100, 10)
    .endFill()
    .beginFill(0xffffff)
    .moveTo(36, 30)
    .lineTo(36, 70)
    .lineTo(70, 50);

// Position the button
button.x = (app.screen.width - button.width) / 2;
button.y = (app.screen.height - button.height) / 2;

// Enable interactivity on the button
// button.interactive = true;
button.eventMode = "dynamic"
button.cursor = 'pointer';

// Add to the stage
app.stage.addChild(button);

// Listen for a click/tap event to start playing the video
// this is useful for some mobile platforms. For example:
// ios9 and under cannot render videos in PIXI without a
// polyfill - https://github.com/bfred-it/iphone-inline-video
// ios10 and above require a click/tap event to render videos
// that contain audio in PIXI. Videos with no audio track do
// not have this requirement
button.on('pointertap', onPlayVideo);

    });

    function onPlayVideo()
{
    // Don't need the button anymore


    // create a video texture from a path
    const texture = PIXI.Texture.from('https://kolown.net/server2/cmyka.mp4');
texture.baseTexture.resource.source.loop = true;

    // create a new Sprite using the video texture (yes it's that easy)
    const videoSprite = new PIXI.Sprite(texture);

    // Stetch the fullscreen
    videoSprite.width = app.screen.width;
    videoSprite.height = app.screen.height;

    app.stage.addChild(videoSprite);
    console.log("ready")
}



</script>
<body>
    <canvas id="canvas" />
</body>



<style>
    #canvas {
        overflow: hidden;
      position: fixed;
      top: 0;
      left: 0;
}


</style>