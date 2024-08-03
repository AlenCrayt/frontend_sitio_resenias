<script lang="ts">
  import { onMount } from "svelte";
  import Close from "svelte-google-materialdesign-icons/Close.svelte";
  import Question_mark from "svelte-google-materialdesign-icons/Question_mark.svelte";

  const patron_url = /^(https?:\/\/)?([\w\-]+(\.[\w\-]+)+\/?)\S*$/;
  let mal_titulo = false;
  let mal_link = false;
  let mal_resenia = false;
  export let es_visible = false;
  let panel_info_copiado_url: HTMLDivElement;
  const resenia = {
    titulo_libro: "",
    link_portada: "",
    resenia_parrafo: "",
  };

  onMount(() => {
    panel_info_copiado_url.style.visibility = "hidden";
  });

  function subir_datos(evento: Event) {
    evento.preventDefault();
    if (resenia.titulo_libro.length < 2) {
      mal_titulo = true;
      return;
    } else {
      mal_titulo = false;
    }
    if (
      resenia.resenia_parrafo.length < 500 ||
      resenia.resenia_parrafo.length > 2000
    ) {
      mal_resenia = true;
      return;
    } else {
      mal_resenia = false;
    }
    if (!patron_url.test(resenia.link_portada.trim())) {
      mal_link = true;
      return;
    } else {
      mal_link = false;
    }
    fetch("http://192.168.1.13:8080/resenias-nuevas", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(resenia),
    });
    alert("Subido exitosamente");
    window.scrollTo(0, 0);
    location.reload();
  }

  function cierre() {
    if (es_visible) {
      es_visible = false;
    } else {
      es_visible = true;
    }
  }

  function sobre_circulo_info() {
    panel_info_copiado_url.style.visibility = "visible";
  }
  function fuera_de_circulo_info() {
    panel_info_copiado_url.style.visibility = "hidden";
  }
</script>

<div id="contenedor">
  <article>
    <div id="boton_cierre">
      <button on:click={cierre}>
        <Close size={"36"} />
      </button>
    </div>
    <h1>Subí tu Reseña</h1>
    <form on:submit={subir_datos}>
      <div id="linea_horizontal">
        <label for="titulo">Titulo del Libro:</label>
        {#if mal_titulo}
          <p id="datos_invalidos">
            El titulo de la novela debe tener dos caracteres como mínimo
          </p>
        {/if}
      </div>
      <input id="titulo" type="text" bind:value={resenia.titulo_libro} />
      <div id="linea_horizontal">
        <label for="link_imagen"
          >Link a una imagen de la portada del libro:</label
        >
        {#if mal_link}
          <p id="link_invalido">Link Invalido</p>
        {/if}
        <div>
          <Question_mark
            on:mouseenter={sobre_circulo_info}
            on:mouseleave={fuera_de_circulo_info}
          />
        </div>
      </div>
      <input id="link_imagen" type="text" bind:value={resenia.link_portada} />
      <div id="linea_horizontal">
        <label for="resenia">Tu Reseña:</label>
        {#if mal_resenia}
          <p id="datos_invalidos">
            La reseña debe tener entre 500 y 2500 caracteres
          </p>
        {/if}
      </div>
      <textarea
        id="resenia"
        cols="120"
        rows="10"
        bind:value={resenia.resenia_parrafo}
      ></textarea>
      <button type="submit">Subir Reseña</button>
    </form>
  </article>
  <p bind:this={panel_info_copiado_url}>
    Cuando veas la portada del libro online hace click derecho en la imagen para
    copiar la URL y pegala aca
  </p>
</div>

<style lang="scss">
  $brown: #967e76;
  $light_brown: #d7c0ae;
  $very_light_brown: #eee3cb;

  @mixin columna_flex {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  @mixin error {
    color: rgb(245, 0, 0);
    margin: 0%;
    padding: 0%;
    font-size: 86%;
    width: 70%;
    height: 20%;
  }

  @keyframes moverse_arriba {
    0% {
      opacity: 0;
      transform: translateY(100%);
    }
    100% {
      opacity: 1;
      transform: translateY(0%);
    }
  }

  #contenedor {
    @include columna_flex();
    position: fixed;
    flex-direction: row;
    height: 50%;
    margin-top: 8%;
    margin-left: 14%;
    animation: moverse_arriba 1s;
  }

  article {
    @include columna_flex();
    border: 1px black;
    background-color: $brown;
    border-radius: 5px;
    width: 40%;
    padding-top: 0;
    padding-bottom: 0;
    padding-left: 1%;
    padding-right: 1%;
  }

  #boton_cierre {
    display: flex;
    justify-content: start;
    align-items: start;
    width: 110%;
    height: 0.1%;
    margin-top: 0;
    margin-bottom: 0;
    button {
      border-radius: 50px;
      margin-top: 0;
      margin-bottom: 0;
      background: none;
      width: 9%;
      height: 0.1%;
    }
  }

  h1 {
    margin-top: 0;
    margin-bottom: 0;
    font-size: 220%;
  }

  form {
    @include columna_flex();
    align-items: start;
    margin-right: 2%;
  }

  #datos_invalidos {
    @include error();
  }

  #link_invalido {
    @include error();
    width: 20%;
  }

  label {
    font-size: 120%;
    margin: 5px;
  }

  input {
    margin: 5px;
    width: 100%;
  }

  #linea_horizontal {
    display: flex;
    flex-direction: row;
    justify-content: start;
    align-items: center;
    padding: 0%;
    margin: 0%;
    width: 100%;
    height: 10%;
    div {
      background-color: $light_brown;
      border-radius: 25px;
    }
  }

  p {
    background-color: $brown;
    color: rgb(50, 50, 50);
    border-radius: 10px;
    width: 20%;
    height: 30%;
    padding: 0.5%;
    margin-bottom: 18%;
    margin-left: 1%;
  }

  textarea {
    font-size: 120%;
    width: 100%;
    padding-bottom: 25%;
    resize: none;
  }

  button {
    font-size: 130%;
    margin: 2%;
    padding: 3%;
    width: 40%;
    border: none;
    border-radius: 15px;
    background-color: $light_brown;
  }

  @media (min-width: 651px) and (max-width: 1000px) and (max-height: 650px) {
    #contenedor {
      margin-top: 5%;
      font-size: 8px;
      article {
        form {
          textarea {
            height: 80px;
            padding: 0;
          }
        }
      }
    }
  }

  @media (min-width: 901px) and (max-width: 1366px) and (min-height: 640px) {
    #contenedor {
      margin-top: 12%;
      height: 30%;
    }
  }

  @media (max-width: 650px) {
    #contenedor {
      width: 240%;
    }
    article {
      margin-right: 50%;
      margin-bottom: 10%;
    }
  }
</style>
