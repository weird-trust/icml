<script>
  import { onMount, onDestroy } from "svelte";
  import p5 from "p5";

  let sketch;
  let canvas;
  let img;
  let glitchImage;
  let posX = 0;
  let posY = 0;

  function glitchEffect(p) {
    p.preload = () => {
      img = p.loadImage("/images/party.gif");
    };

    p.setup = () => {
      canvas = p.createCanvas(p.windowWidth, p.windowHeight);
      p.noCursor();
    };

    p.draw = () => {
      p.image(img, posX, posY, 150, 150); // Größe des Bildes anpassen
      applyGlitch();
    };

    function applyGlitch() {
      let x = p.random(p.width);
      let y = p.random(p.height);
      let w = p.random(10, 100);
      let h = p.random(10, 100);
      glitchImage = img.get(x, y, w, h);
      p.image(glitchImage, posX + p.random(-10, 10), posY + p.random(-10, 10));
    }

    p.mouseMoved = () => {
      posX = p.mouseX - 75; // Zentriere das Bild auf den Cursor
      posY = p.mouseY - 75; // Zentriere das Bild auf den Cursor
    };

    p.windowResized = () => {
      p.resizeCanvas(p.windowWidth, p.windowHeight);
    };
  }

  onMount(() => {
    sketch = new p5(
      glitchEffect,
      document.getElementById("party-mode-container")
    );
  });

  onDestroy(() => {
    if (sketch) {
      sketch.remove();
    }
  });
</script>

<div id="party-mode-container"></div>

<style>
  #party-mode-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
  }
</style>
