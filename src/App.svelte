<script lang="ts">
  let button: HTMLButtonElement;
  let tooltip: HTMLDivElement
</script>

<main>
  <button bind:this={button}>
    My Button
  </button>
  <div role="tooltip" bind:this={tooltip}>My tooltip</div>
</main>

<style lang="scss">
</style>
