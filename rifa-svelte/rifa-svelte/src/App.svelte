<script>
  import InputFinalists from "./InputFinalists.svelte";
  import Bracket from "./Bracket.svelte";

</script>

<svelte:head>
  <style>
    html, body, #app {
      height: 100vh;
      margin: 0;
    }
  </style>
</svelte:head>

<div id="app">
  <InputFinalists />
  <Bracket />
</div>
