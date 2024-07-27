<script lang="ts">
  let lista_libros: Array<any> = [];

  const obtener_json = async () => {
    const datos = await fetch("http://192.168.1.13:8080/resenias-generales");
    if (datos.ok) {
      return datos.json();
    }
  };

  const result = obtener_json();
  result.then((data) => {
    lista_libros = data;
  });
  //Hay que agregar al código la posibilidad de poder manejar el error de contactar al servidor y no recibir ningún dato
</script>

<main>
  {#each lista_libros as libro}
    <article>
      <div>
        <h2>{libro.titulo}</h2>
        <p>{libro.parrafo}</p>
      </div>
      <img src={libro.link_imagen} alt="Imagen no disponible" />
    </article>
  {/each}
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
</style>
