<script>
  // let finalists = $state(['', '', '', '', '', '', '', '']);
  import { finalists, eventBus } from "./sharedState.svelte";
  let available_positions = $state([0,1,2,3,4,5,6,7]);
  let nombre = $state("");
  let error = $state("");
  $inspect(finalists)

  function distributeFinalists(nombre) {
    if (checkDouble(nombre) === true) {
      return;
    };

    if (available_positions.length === 0) {
      error = "Todos los finalistas han estado selecionados."
      return;
    };

    const randomIndex = Math.floor(Math.random() * available_positions.length);
    const ind = available_positions[randomIndex];
    const new_ap = available_positions.filter(elem => elem !== available_positions[randomIndex]);
    available_positions = new_ap;

    finalists[ind] = nombre;
    $state.snapshot(finalists)

    eventBus.set({ind: ind, nombre: nombre});
  }

  function checkDouble(nombre) {
    for (const finalist of finalists) {
      if (finalist === nombre) {
        return true;
      }
    }
    return false;
  }

</script>

<style>
  .input-finalists {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 100%;
    z-index: 1;
    position: absolute;
    background-color: transparent;
  }

  .form {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 1px solid grey;
    padding: 1rem;
    border-radius: 15px;
    background-color: white;
  }

  .form-label {
    margin-bottom: 0.5rem;
  }

  .form-input {
    border-radius: 15px;
    width: 100%;
    margin-bottom: 0.5rem;
    border: 1px solid grey;
  }

  .form-button {
    border-radius: 15px;
    border: 1px solid grey;
    width: 50%;
  }

</style>

<div class="input-finalists">
  <form class="form">
    <label
      for="finalista"
      class="form-label">
        Ingrese los finalistas por favor señorita
    </label>
    <input
      type='text'
      id="finalista"
      class="form-input"
      placeholder="Nombre"
      bind:value={nombre}/>
    <button
      type="button"
      class="form-button"
      onclick={() => distributeFinalists(nombre)}>
        Ingresar
    </button>
  </form>
  <!-- {#each finalists as finalist}
    <p>{finalist}</p>
  {/each}
  <p>{error}</p> -->
</div>
