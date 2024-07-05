<script>
  import BarraSuperior from "./barra_superior.svelte";
  import ListaResenias from "./lista_resenias.svelte";
</script>

<div>
  <BarraSuperior />
  <ListaResenias />
</div>

<style lang="scss">
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
    color: #d7c0ae;
    background-color: #b7c4cf;
  }
</style>
