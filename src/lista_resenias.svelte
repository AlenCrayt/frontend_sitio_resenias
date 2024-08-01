<script lang="ts">
  import { onMount } from "svelte";
  import Chevron_right from "svelte-google-materialdesign-icons/Chevron_right.svelte";
  import Chevron_left from "svelte-google-materialdesign-icons/Chevron_left.svelte";

  let cantidad_por_pagina = 5;
  let contador_guardado = sessionStorage.getItem("contador") as string;
  let contador_paginas = JSON.parse(contador_guardado) as number;
  export let lista_libros: Array<any> = [];

  onMount(async () => {
    window.scrollTo(0, 0);
    try {
      const datos_resenias = await fetch(
        `http://192.168.1.13:8080/resenias-generales?indice=${contador_paginas}`
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

  function pasa_de_pagina(retroceder: boolean) {
    if (retroceder) {
      contador_paginas -= cantidad_por_pagina;
    } else {
      contador_paginas += cantidad_por_pagina;
    }
    fetch(
      `http://192.168.1.13:8080/resenias-generales?indice=${contador_paginas}`,
      {
        method: "GET",
      }
    )
      .then((response) => {
        if (response.status == 404) {
          if (retroceder) {
            contador_paginas += cantidad_por_pagina;
          } else {
            contador_paginas -= cantidad_por_pagina;
          }
        }
        return response.json();
      })
      .then((data) => {
        lista_libros = data;
        sessionStorage.setItem("contador", JSON.stringify(contador_paginas));
        window.scrollTo(0, 0);
      });
  }
</script>

<main>
  {#if lista_libros.length > 0}
    {#each lista_libros as libro}
      <article>
        <div>
          <h2>{libro.titulo_libro}</h2>
          <p>{libro.resenia_parrafo}</p>
        </div>
        <img src={libro.link_portada} alt="Imagen no disponible" />
      </article>
    {/each}
    <div id="contenedor_flex">
      {#if contador_paginas >= cantidad_por_pagina}
        <button id="chevrones" on:click={() => pasa_de_pagina(true)}
          ><Chevron_left size={"60"} /></button
        >
      {/if}
      <button id="chevrones" on:click={() => pasa_de_pagina(false)}
        ><Chevron_right size={"60"} /></button
      >
    </div>
  {:else}
    <h1>No hay Reseñas todavía!</h1>
  {/if}
</main>

<style lang="scss">
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
    background-color: #b2a3ff;
    border-radius: 20px;
    margin: 15px;
    box-shadow: 5px 5px rgb(50, 50, 50);
  }

  div {
    grid-column: 2;
    grid-row: 1;
    margin-left: 20px;
    margin-right: 20px;
  }

  h2 {
    font-size: 200%;
    margin: 0%;
  }

  img {
    grid-column: 1;
    grid-row: 1;
    width: 175px;
    height: 262px;
    margin: 15px;
  }

  #contenedor_flex {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #chevrones {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0%;
    margin-left: 10%;
    background-color: #b2a3ff;
    border: none;
    border-radius: 100%;
    height: 65px;
    width: 80px;
  }

  h1 {
    color: rgb(50, 50, 50);
  }
</style>
