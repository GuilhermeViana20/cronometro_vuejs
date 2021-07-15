<template>
  <div id="app">

    <img class="img" alt="Vue logo" src="./assets/cronometro.png">

    <a class="timer" href="">00:00,00</a>

    <div class="areaBtn">
      <button class="botao">INICIAR</button>
      <button class="botao">REINICIAR</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App'
}
</script>

<style>
  #app {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .img {
    width: 420px;
    height: auto;
    padding-top: 100px;
  }

  .timer {
    color: #a435f0;
    font-size: 70px;
    margin-top: -250px;
    text-decoration: none;
  }

  .areaBtn {
    margin-top: 200px;
  }

  .botao {
    -webkit-user-select: none;
    -moz-user-select: none;
    width: 150px;
    background-color: #a435f0;
    color: white;
    font-weight: 700;
    font-size: 20px;
    border: 0;
    border-radius: 5px;
    text-align: center;
    margin-left: 15px;
    margin-right: 15px;
    padding: 10px;
    cursor: pointer;
  }

  .botao:hover {
    opacity: 0.7;
    transform: scale(1.1);
    transition: all 300ms;
  }
</style>
