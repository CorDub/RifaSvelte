<script>
  let {position} = $props();
  import { finalists, eventBus } from "./sharedState.svelte";
  let nombre = $state(finalists[position]);

  eventBus.subscribe((value) => {
    if (value.ind === position) {
      nombre = value.nombre;
      $state.snapshot(nombre);
    }
  })
</script>

<style>
  p {
    margin: 0;
    font-size: 1.5em;
    color: red;
  }
</style>

<div class="one-on-one">

  {#if nombre}
    <p>{nombre}</p>
  {:else}
    <p> This is position {position}</p>
  {/if}
</div>
