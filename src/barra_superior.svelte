<script lang="ts">
  //Los métodos de busca y leída de la base de datos van a estar disponibles a todos los visitantes de la pagina no solo usuarios registrados
  export let ver_panel = false;
  export let busca_texto = "";

  function mostrar_panel_subida() {
    if (ver_panel == false) {
      ver_panel = true;
    }
  }
  const buscar = () => {
    busca_texto = document.querySelector("input")?.value as string;
  };
  //Agregar antes de construir la version de producción agregar un <a> que dirige a la URL inicial de la pagina
</script>

<nav>
  <a href="http://192.168.1.13:8080/">Reseñas</a>
  <div class="barra_busqueda">
    <input type="search" />
    <button on:click={buscar}>
      <img src="src\assets\icono_busqueda.svg" alt="imagen no disponible" />
    </button>
  </div>
  <button id="subida_resenia" on:click={mostrar_panel_subida}
    >Subí tu Reseña</button
  >
</nav>

<style lang="scss">
  $brown: #967e76;
  $light_brown: #d7c0ae;
  $very_light_brown: #eee3cb;

  nav {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    color: black;
    margin-top: 8px;

    a {
      font-size: 32px;
      margin: 0;
      padding: 0;
      text-decoration: none;
      color: black;
    }

    .barra_busqueda {
      display: flex;
      justify-content: center;
      align-items: center;
      input {
        border: none;
        border-radius: 10px;
        width: 300px;
        height: 30px;
      }
    }

    button {
      border: none;
      border-radius: 25px;
      background-color: $brown;
      margin-left: 5px;
    }

    #subida_resenia {
      color: $very_light_brown;
      font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
      font-size: 140%;
      padding-right: 1%;
      padding-left: 1%;
      padding-bottom: 0.2%;
      padding-top: 0.2%;
    }
  }
</style>
