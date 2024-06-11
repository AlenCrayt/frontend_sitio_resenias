<script lang="ts">
  const manejar_subida = async (evento: Event) => {
    const formulario = evento.target as HTMLFormElement;
    const datos_a_enviar = new FormData(formulario);
    fetch("http://192.168.1.12:8080/agregar_resenias", {
      method: "POST",
      body: datos_a_enviar,
    });
  };
</script>

<div class="container">
  <div></div>
  <div class="subida">
    <details>
      <summary>Subi tu reseña</summary>
      <form method="post" on:submit|preventDefault={manejar_subida}>
        <label for="titulo">Titulo:</label>
        <input type="text" name="titulo" id="titulo" />
        <label for="link_imagen"
          >Link a una imagen de la portada del libro:</label
        >
        <input type="text" name="link_img" id="link_imagen" />
        <label for="parrafo">Reseña:</label>
        <input type="text" name="parrafo" id="parrafo" />
        <button type="submit">Subir Reseña</button>
      </form>
    </details>
  </div>
  <div></div>
</div>

<style lang="scss">
  $brown: #967e76;
  $light_brown: #d7c0ae;
  $very_light_brown: #eee3cb;

  @mixin columna_flex {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .container {
    @include columna_flex;
  }

  .subida {
    @include columna_flex;
    font-size: 20px;
    border: none;
    background-color: $light_brown;
    border-radius: 25px;
    color: white;
    padding: 8px;
  }

  form {
    @include columna_flex;
  }
</style>
