<script lang="ts">
  //Los métodos de busca y leída de la base de datos van a estar disponibles a todos los visitantes de la pagina no solo usuarios registrados
  export let resultados_busqueda: Array<any> = [];
  const realizar_busqueda = async () => {
    const termino_busqueda = document.querySelector("input")?.value;
    fetch(
      `http://192.168.1.13:8080/resenias-especificas?buscar-titulo=${termino_busqueda}`,
      {
        method: "GET",
      }
    )
      .then((respuesta) => {
        return respuesta.json();
      })
      .then((datos) => {
        resultados_busqueda = datos;
      });
  };
</script>

<nav>
  <h1>Reseñas</h1>
  <div class="barra_busqueda">
    <input type="search" />
    <button on:click={realizar_busqueda}>
      <img src="src\assets\icono_busqueda.svg" alt="imagen no disponible" />
    </button>
  </div>
  <li>
    <h2>Usuario</h2>
    <ul>
      <li class="opciones_cuenta">Registrarse</li>
      <li class="opciones_cuenta">Ingresar</li>
    </ul>
  </li>
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

    h1 {
      font-size: 32px;
      margin: 0;
      padding: 0;
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

    li {
      display: flex;
      justify-content: center;
      flex-direction: column;
      margin-right: 15px;
      padding: 0;
    }

    h2 {
      margin: 0;
      padding: 0;
    }

    ul {
      visibility: hidden;
      list-style: none;
      margin: 0;
      padding: 0;
      border-radius: 5px;
      background-color: $light_brown;
      li {
        margin: 0;
        padding: 5px;
      }
    }

    li:hover ul {
      visibility: visible;
    }
  }
</style>
