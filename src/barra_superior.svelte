<script lang="ts">
</script>

<nav>
  <h1>Reseñas</h1>
  <button>Subi tu Reseña</button>
</nav>

<style lang="scss">
  $brown: #967e76;
  $light_brown: #d7c0ae;
  $very_light_brown: #eee3cb;

  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid black;
    background-color: $brown;
    color: $very_light_brown;
    h1 {
      font-size: 32px;
      margin: 6px;
    }
  }

  button {
    font-size: 20px;
    border: none;
    background-color: $light_brown;
    border-radius: 25px;
    color: white;
    padding: 8px;
  }
</style>
