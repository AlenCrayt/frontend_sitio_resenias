<script lang="ts">
  import BarraSuperior from "./barra_superior.svelte";
  import ListaResenias from "./lista_resenias.svelte";
  import FormularioResenias from "./formulario_resenias.svelte";

  let panel_subida_es_visible = false;
  let termino_busqueda_global = "";
  $: {
    if (termino_busqueda_global != "") {
      fetch(
        `http://192.168.1.13:8080/resenias-especificas?buscar-titulo=${termino_busqueda_global}`,
        {
          method: "GET",
        }
      )
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          console.log(data);
        });
    }
  }
</script>

<div>
  <BarraSuperior
    bind:busca_texto={termino_busqueda_global}
    bind:ver_panel={panel_subida_es_visible}
  />
  {#if panel_subida_es_visible}
    <FormularioResenias bind:es_visible={panel_subida_es_visible} />
  {/if}
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
