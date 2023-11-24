<script lang="ts">
  import Control from "./lib/Control.svelte";

  let [a, b, c, d, e, f] = [1, 0, 0, 1, 0, 0];
  let width = 600;
  let height = 400;

  function pan(dx: number, dy: number) {
    e += dx;
    f += dy;
  }

  function zoom(scale: number) {
    a *= scale;
    b *= scale;
    c *= scale;
    d *= scale;

    e += ((1 - scale) * width) / 2;
    f += ((1 - scale) * height) / 2;
  }
</script>

<main>
  <h1>Toto</h1>

  <button on:click={() => pan(0, -25)}>Haut</button>
  <button on:click={() => pan(-25, 0)}>Gauche</button>
  <button on:click={() => pan(25, 0)}>Droite</button>
  <button on:click={() => pan(0, 25)}>Bas</button>
  <button on:click={() => zoom(1.25)}>+</button>
  <button on:click={() => zoom(0.8)}>-</button>

  <svg {width} {height}>
    <g {width} {height} transform="matrix({a} {b} {c} {d} {e} {f})">
      <image xlink:href="/38-306.jpeg" x="0" y="0" />

      <Control />
    </g>
  </svg>
</main>

<style>
  svg {
    background-color: grey;
    border: 2px solid black;
    cursor: move;
  }
</style>
