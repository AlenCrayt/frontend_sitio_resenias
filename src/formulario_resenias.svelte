<script lang="ts">
  let en_vista = false;
  const panel_subida = document.querySelector("article") as HTMLElement;
  //Se esta aplicando la propiedad de visibility a todos los elementos por alguna razon
  /*if (en_vista) {
    panel_subida.style.visibility = "visible";
  } else {
    panel_subida.style.visibility = "hidden";
  }*/
  //Sacar una captura de pantalla haciendo click derecho en una imagen de una portada para mostrar un ejemplo de como copiar la URL de una imagen
</script>

<div>
  <article>
    <div id="boton_cierre">
      <img src="src/assets/cerrar.svg" alt="imagen no disponible" />
    </div>
    <h1>Subí tu Reseña</h1>
    <form>
      <label for="titulo">Titulo del Libro:</label>
      <input id="titulo" type="text" />
      <div id="linea_horizontal">
        <label for="link_imagen"
          >Link a una imagen de la portada del libro:</label
        >
        <img src="src/assets/simbolo_pregunta.svg" alt="imagen no disponible" />
      </div>
      <input id="link_imagen" type="text" />
      <label for="resenia">Su Reseña:</label>
      <textarea id="resenia" cols="120" rows="10"></textarea>
      <button>Subir Reseña</button>
    </form>
  </article>
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

  div {
    @include columna_flex();
  }

  article {
    @include columna_flex();
    border: 1px black;
    border-radius: 5px;
    background-color: $brown;
    width: 30%;
    padding: 1%;
  }

  #boton_cierre {
    display: flex;
    align-items: end;
    width: 100%;
    img {
      background-color: $light_brown;
      padding: 1%;
      width: 4%;
      height: 4%;
      border-radius: 15px;
    }
  }

  h1 {
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

  #informacion {
    border-radius: 100%;
  }

  img {
    background-color: $light_brown;
    border-radius: 10px;
    padding: 0.5%;
    width: 4%;
    height: 4%;
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
