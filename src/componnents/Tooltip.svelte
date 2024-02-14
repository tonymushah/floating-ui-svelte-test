<script lang="ts">
  import { flip, offset, arrow } from "@floating-ui/dom";
  import { shift } from "@floating-ui/dom";
  import { computePosition } from "@floating-ui/dom";
  import "@fontsource/poppins/devanagari.css";
  import { onMount } from "svelte";
  let button: HTMLButtonElement;
  let tooltip: HTMLDivElement;
  let arrowElement: HTMLDivElement;
  onMount(async () => {
    const { x, y, placement, middlewareData } = await computePosition(
      button,
      tooltip,
      {
        placement: "top",
        middleware: [
          offset(6),
          flip(),
          shift({
            padding: 5,
          }),
          arrow({
            element: arrowElement,
          }),
        ],
      }
    );
    Object.assign(tooltip.style, {
      left: `${x}px`,
      top: `${y}px`,
    });
    const { x: arrowX, y: arrowY } = middlewareData.arrow;
    const staticSide = {
      top: "bottom",
      right: "left",
      bottom: "top",
      left: "right",
    }[placement.split("-")[0]];

    Object.assign(arrowElement.style, {
      left: arrowX != null ? `${arrowX}px` : "",
      top: arrowY != null ? `${arrowY}px` : "",
      right: "",
      bottom: "",
      [staticSide]: "-4px",
    });
  });
</script>

<main>
  <button class:button bind:this={button} aria-labelledby="button-tooltip">
    My Button
  </button>
  <div id="button-tooltip" class:tooltip role="tooltip" bind:this={tooltip}>
    My tooltip with more content
    <div class="arrow" bind:this={arrowElement} />
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
  .arrow {
    position: absolute;
    background: #222;
    width: 8px;
    height: 8px;
    transform: rotate(45deg);
  }
</style>
