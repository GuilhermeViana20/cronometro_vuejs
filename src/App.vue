<template>
  <div id="app">

    <img class="img" alt="Vue logo" src="./assets/cronometro.png">

    <a class="timer" href="">{{numero}}</a>

    <div class="areaBtn">
      <button class="botao" @click="iniciar">{{botao}}</button>
      <button class="botao" @click="reiniciar">REINICIAR</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      numero: '00:00.00',
      botao: 'INICIAR',
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
    }
  },
  methods: {
    iniciar() {
      if(this.timer !== null){
        // TIMER NÃO É NULO
        clearInterval(this.timer);
        this.timer = null;
        this.botao = 'INICIAR';
      } else {
        // TIMER É NULO

        this.timer = setInterval(()=> {
          this.rodarTimer();
        }, 0.1) // 1seg
        this.botao = 'PAUSAR';
      }
    },
    reiniciar() {
      this.timer = '00:00.00';
    },
    rodarTimer() {
      this.ss++;

      if(this.ss == 59) {
        // 59 Segundos
        this.ss = 0;
        this.mm++;
      }

      if(this.mm == 59) {
        // 59 Minutos
        this.mm = 0;
        this.hh++;
      }

      let format = (this.hh < 10 ? '0'+this.hh : this.hh) + ':'
      + (this.mm < 10 ? '0' + this.mm : this.mm) + '.'
      + (this.ss < 10 ? '0' + this.ss : this.ss);

      return this.numero = format;
    }
  }
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