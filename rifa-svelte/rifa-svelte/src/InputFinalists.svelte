<script>
  let finalists = $state(['', '', '', '', '', '', '', '']);
  let available_positions = $state([0,1,2,3,4,5,6,7]);
  let nombre = $state("");
  let error = $state("");

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

    const newArray = [...finalists]
    newArray[ind] = nombre;
    finalists = newArray;
  }

  function checkDouble(nombre) {
    for (const finalist of finalists) {
      if (nombre === finalist) {
        error = "Este finalista ya esta ingresado."
        return true;
      }
    }
    return false;
  }
</script>

<div class="input-finalists">
  <form>
    <label for="finalista">Ingrese los finalistas por favor señorita</label>
    <input type='text' id="finalista" placeholder="Nombre del finalista" bind:value={nombre}/>
    <button type="button" onclick={() => distributeFinalists(nombre)}>Ingresar</button>
  </form>
  {#each finalists as finalist}
    <p>{finalist}</p>
  {/each}
  <p>{error}</p>
</div>
