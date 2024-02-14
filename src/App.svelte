<script lang="ts">
  let button: HTMLButtonElement;
  let tooltip: HTMLDivElement
</script>

<main>
  <button class:button bind:this={button} aria-labelledby="button-tooltip">
    My Button
  </button>
  <div id="button-tooltip" class:tooltip role="tooltip" bind:this={tooltip}>My tooltip</div>
</main>

<style lang="scss">
  
</style>
