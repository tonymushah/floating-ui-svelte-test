<script lang="ts">
  import { computePosition } from "@floating-ui/dom";
  import "@fontsource/poppins/devanagari.css";
  import { onMount } from "svelte";
  let button: HTMLButtonElement;
  let tooltip: HTMLDivElement;
  onMount(async () => {
    let { x, y } = await computePosition(button, tooltip, {
      placement: "right",
    });
    Object.assign(tooltip.style, {
      left: `${x}px`,
      top: `${y}px`,
    });
  });
</script>

<main>
  <button class:button bind:this={button} aria-labelledby="button-tooltip">
    My Button
  </button>
  <div id="button-tooltip" class:tooltip role="tooltip" bind:this={tooltip}>
    My tooltip
  </div>
</main>

<style lang="scss">
  div {
    font-family: inherit;
  }
  button {
    font-family: inherit;
    background-color: #ddd;
    border-radius: 4px;
    padding: 5px 10px;
    font-weight: 700;
    font-size: medium;
  }
  .tooltip {
    background: #222;
    color: white;
    font-weight: bold;
    padding: 5px;
    border-radius: 4px;
    font-size: 90%;
    width: max-content;
    position: absolute;
    top: 0;
    left: 0;
  }
  main {
    font-family: "Poppins", sans-serif;
  }
</style>
