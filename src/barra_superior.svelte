<script lang="ts">
  import Search from "svelte-google-materialdesign-icons/Search.svelte";
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
</script>

<nav>
  <a href="http://192.168.1.13:8080/">Reseñas</a>
  <div class="barra_busqueda">
    <input type="search" />
    <button on:click={buscar}>
      <Search />
    </button>
  </div>
  <button id="subida_resenia" on:click={mostrar_panel_subida}
    >Subí tu Reseña</button
  >
</nav>

<style lang="scss">
  @media (max-width: 650px) {
    nav {
      flex-direction: column;
    }
    #subida_resenia {
      margin-top: 3%;
    }
  }

  nav {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-top: 8px;

    a {
      color: rgb(50, 50, 50);
      font-size: 300%;
      margin: 0;
      padding: 0;
      text-decoration: none;
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
      color: rgb(50, 50, 50);
      background-color: #b2a3ff;
      margin-left: 5px;
    }

    #subida_resenia {
      font-size: 140%;
      padding-right: 1%;
      padding-left: 1%;
      padding-bottom: 0.2%;
      padding-top: 0.2%;
    }
  }
</style>
