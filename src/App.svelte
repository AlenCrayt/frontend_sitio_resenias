<script lang="ts">
  import BarraSuperior from "./barra_superior.svelte";
  import ListaResenias from "./lista_resenias.svelte";
  import FormularioResenias from "./formulario_resenias.svelte";

  let panel_subida_es_visible = false;
  let termino_busqueda_global = "";
  let resultado_de_busqueda: Array<any> = [];
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
          resultado_de_busqueda = data;
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
  <ListaResenias bind:lista_libros={resultado_de_busqueda} />
</div>

<style lang="scss">
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: sans-serif;
    color: rgb(50, 50, 50);
    background-image: url(https://i.pinimg.com/originals/bf/af/59/bfaf59c73409c1aea2457219b2b3c64f.jpg);
    background-size: contain;
  }
</style>
