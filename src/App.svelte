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
    font-family: Georgia, "Times New Roman", Times, serif;
    color: #d7c0ae;
    background-color: #b7c4cf;
  }
</style>
