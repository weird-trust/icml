<script>
  import { onMount, onDestroy } from "svelte";
  import p5 from "p5";

  let sketch;
  let posX = 100;
  let posY = 100;
  let speedX = 2;
  let speedY = 2;
  let isDragging = false;
  let offsetX = 0;
  let offsetY = 0;

  onMount(() => {
    const s = (p) => {
      p.setup = () => {
        p.createCanvas(p.windowWidth, p.windowHeight);
      };

      p.mousePressed = () => {
        if (
          p.mouseX > posX &&
          p.mouseX < posX + 300 &&
          p.mouseY > posY &&
          p.mouseY < posY + 20
        ) {
          isDragging = true;
          offsetX = p.mouseX - posX;
          offsetY = p.mouseY - posY;
        }
      };

      p.mouseDragged = () => {
        if (isDragging) {
          posX = p.mouseX - offsetX;
          posY = p.mouseY - offsetY;
        }
      };

      p.mouseReleased = () => {
        isDragging = false;
      };

      p.windowResized = () => {
        p.resizeCanvas(p.windowWidth, p.windowHeight);
      };
    };

    sketch = new p5(s, document.getElementById("glitch-container"));
  });

  onDestroy(() => {
    if (sketch) {
      sketch.remove();
    }
  });
</script>

<div id="glitch-container"></div>

<style>
  #glitch-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 0; /* Hinter dem Player */
    background-color: rgb(14, 110, 110);
  }
</style>
