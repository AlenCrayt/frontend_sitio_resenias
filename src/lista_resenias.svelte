<script lang="ts">
  import { onMount } from "svelte";

  let lista_libros: Array<any> = [];

  onMount(async () => {
    try {
      const datos_resenias = await fetch(
        "http://192.168.1.13:8080/resenias-generales"
      );
      if (!datos_resenias.ok) {
        throw new Error(`Hubo un error de HTTP: ${datos_resenias.status}`);
      }
      let reserva_temporal = await datos_resenias.json();
      if (
        reserva_temporal === null ||
        reserva_temporal === undefined ||
        reserva_temporal.length === 0
      ) {
        throw new Error("La respuesta esta vacía de datos o es null");
      }
      lista_libros = reserva_temporal;
    } catch {
      console.log("Ocurrió un error al recibir los datos del servidor");
    }
  });
</script>

<main>
  {#if lista_libros.length > 0}
    {#each lista_libros as libro}
      <article>
        <div>
          <h2>{libro.titulo}</h2>
          <p>{libro.parrafo}</p>
        </div>
        <img src={libro.link_imagen} alt="Imagen no disponible" />
      </article>
    {/each}
  {:else}
    <h1>No hay Reseñas todavía!</h1>
  {/if}
</main>

<style lang="scss">
  $brown: #967e76;
  $light_brown: #d7c0ae;
  $very_light_brown: #eee3cb;

  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 30px;
  }

  article {
    display: grid;
    grid-template-columns: 2;
    grid-template-rows: 1;
    background-color: $brown;
    border-radius: 20px;
    margin: 15px;
  }

  div {
    grid-column: 2;
    grid-row: 1;
    margin-left: 20px;
    margin-right: 20px;
  }

  img {
    grid-column: 1;
    grid-row: 1;
    width: 175px;
    height: 262px;
    margin: 15px;
  }

  h1 {
    color: black;
  }
</style>
