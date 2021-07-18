<template>
  <div id="app">

    <img class="img" alt="Vue logo" src="./assets/cronometro.png">

    <a class="timer" href="">{{numero}}</a>

    <div class="areaBtn">
      <button class="botao" @click="iniciar">{{botao}}</button>
      <button class="botao" @click="reiniciar">REINICIAR</button>
    </div>

    <div class="list" v-show="historico.length > 0">
      <ul>
        <li v-for="item in historico" :key="item">Você fez uma pausa em {{item}}</li>
      </ul>

      <button class="botao-historico" @click="historico = []">LIMPAR HISTÓRICO</button>
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
      historico: []
    }
  },
  methods: {
    iniciar() {
      if(this.timer !== null){
        // TIMER NÃO É NULO
        clearInterval(this.timer);
        this.timer = null;
        this.botao = 'INICIAR';
        if(this.ss !== 0) {
          this.historico.push(this.numero);
        }
      } else {
        // TIMER É NULO

        this.timer = setInterval(()=> {
          this.rodarTimer();
        }, 100) // 1seg
        this.botao = 'PAUSAR';
      }
    },
    reiniciar() {
      if(this.timer !== null) {
        clearInterval(this.timer);
        this.timer = null;
      }
      this.ss = 0;
      this.mm = 0;
      this.hh = 0;
      this.numero = '00:00.00';
      this.botao = 'INICIAR';
      this.historico = [];
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

  .list ul {
    text-align: center;
    padding: 0;
  }

  .list ul li {
    margin-top: 4px;
    padding: 25px;
    background-color: #ccc;
    list-style: none;
    color: #a435f0;
    font-size: 18px;
    font-weight: 600;
    border-radius: 5px;
    margin-bottom: 12px;
  }

  .botao-historico {
    -webkit-user-select: none;
    -moz-user-select: none;
    width: 100%;
    background-color: #3a0a5a;
    color: white;
    font-weight: 700;
    font-size: 20px;
    border: 0;
    border-radius: 5px;
    text-align: center;
    padding: 10px;
    cursor: pointer;
  }

  .botao-historico:hover {
    opacity: 0.7;
    transform: scale(1.1);
    transition: all 300ms;
  }
</style>