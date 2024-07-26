<script lang="ts">
  import { onMount } from "svelte";

  export let es_visible = false;
  let panel_info_copiado_url: HTMLDivElement;
  /*let panel_subida: HTMLElement;*/

  onMount(() => {
    panel_info_copiado_url.style.visibility = "hidden";
  });

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
  //Sacar una captura de pantalla haciendo click derecho en una imagen de una portada para mostrar un ejemplo de como copiar la URL de una imagen
</script>

<div id="contenedor">
  <article>
    <div id="boton_cierre">
      <button on:click={cierre}>
        <img src="src/assets/cerrar.svg" alt="imagen no disponible" />
      </button>
    </div>
    <h1>Subí tu Reseña</h1>
    <form>
      <label for="titulo">Titulo del Libro:</label>
      <input id="titulo" type="text" />
      <div id="linea_horizontal">
        <label for="link_imagen"
          >Link a una imagen de la portada del libro:</label
        >
        <img
          on:mouseenter={sobre_circulo_info}
          on:mouseleave={fuera_de_circulo_info}
          src="src/assets/simbolo_pregunta.svg"
          alt="imagen no disponible"
        />
      </div>
      <input id="link_imagen" type="text" />
      <label for="resenia">Tu Reseña:</label>
      <textarea id="resenia" cols="120" rows="10"></textarea>
      <button>Subir Reseña</button>
    </form>
  </article>
  <p bind:this={panel_info_copiado_url}>
    Cuando veas una portada de un libro online hace click derecho en la imagen
    para copiar la URL y pegala aca
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

  #contenedor {
    @include columna_flex();
    flex-direction: row;
    margin-left: 14%;
  }

  article {
    @include columna_flex();
    border: 1px black;
    border-radius: 5px;
    background-color: $brown;
    width: 30%;
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
      margin-top: 0;
      margin-bottom: 0;
      background: none;
      width: 9%;
      height: 0.1%;
      img {
        border-radius: 50px;
        padding: 50%;
        width: 150%;
        height: 150%;
      }
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
    width: 100%;
  }

  img {
    background-color: $light_brown;
    border-radius: 10px;
    padding: 0.5%;
    width: 4%;
    height: 4%;
  }

  p {
    background-color: $brown;
    color: $light_brown;
    border-radius: 10px;
    width: 20%;
    height: 50%;
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
    font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
    font-size: 130%;
    margin: 2%;
    padding: 3%;
    width: 40%;
    border: none;
    border-radius: 15px;
    background-color: $light_brown;
  }
</style>
