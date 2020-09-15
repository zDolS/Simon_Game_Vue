<template>
      <div class="" id="app">
        <h2 class="title">Simon Game</h2>       
          <div class="info_game">
            <h3 class="round">Раунд: {{round}}</h3>
            <button class="game__start" v-on:click="startGame">start</button>
          </div>
          <div class="game">
            <div class="game-field">
              <button
                  value="1"
                  class="game__btn game__btn__blue"
                  :class="{btn_act: (currentLightBtn === 1)}" 
                  v-on:click="checkBtn(1)"
                > 
              </button>
              <button
                class="game__btn game__btn__red"
                value="2"
                :class="{btn_act: (currentLightBtn === 2)}"
                v-on:click="checkBtn(2)"
              >
              </button>
              <button
                class="game__btn game__btn__yellow"
                value="3"
                :class="{btn_act: (currentLightBtn === 3)}"
                v-on:click="checkBtn(3)"
              > 
              </button>
              <button
                class="game__btn game__btn__green"
                value="4"
                :class="{btn_act: (currentLightBtn === 4)}"
                v-on:click="checkBtn(4)"
              > 
              </button>
            </div>
            <div class="cutout"></div>
          </div>
        </div>
</template>
<script>
export default {
  data() { 
    return {
      currentLightBtn: null,
      round: 1,
      indexStartGame: 0,
      clockCheckGame: 1,
      indexCheckGame: 0,
      stg: [],
      lightBtn: null,
    };
  },

  methods: {
    //начинаем игру, задаем стартовые значения, случайно подсвечиваем сектора круга
    startGame() {
      this.indexStartGame = 0;
      this.clockCheckGame = 1;
      this.indexCheckGame = 0;
      this.btns = document.querySelectorAll(".game__btn");

      for (let i = 0; i < this.round; i++) {
        this.stg[i] = Math.floor(Math.random() * 4) + 1;
      }
        this.lightBtn = setInterval(() => {
        if (this.indexStartGame > this.round) {
          clearInterval(this.lightBtn);
        } else {
          this.currentLightBtn = this.stg[this.indexStartGame];
          this.indexStartGame++;
        }
      }, 1000);
    },

//проверка клика пользователя
  checkBtn(x) {
    if (x != this.stg[this.indexCheckGame]) {
      alert("Вы проиграли!");
      this.round = 1;
      this.currentLightBtn = null;
      this.indexStartGame = 0;
      this.clockCheckGame = 1;
      this.indexCheckGame = 0;
      this.stg = [];
      this.intervalId = null;

    } else {
      if (this.clockCheckGame == this.stg.length) {
        this.currentLightBtn = "";
        this.round++;
        this.stg = [];
        this.startGame();
      } else{
        this.indexCheckGame++;
        this.clockCheckGame++;
      } 
    }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#app {
  font-family: Arial, serif;
  color: #333;
  width: 500px;
  margin: 0 auto;
}

.btn_off {
  background: red;
}
.title{
  margin: 1em 0 2em;
  text-align: center;
}

.info_game{
  float: right;
  margin-top: 70px;
}

.game__start {
  float: right;
  margin-top: 10px;
  width: 5em;
  box-sizing: border-box;
  font-size: 1.4em;
  -webkit-border-radius: 10px 10px 10px 10px;
  border-radius: 10px 10px 10px 10px;
  background: #6DABE8;
  border: none;
  padding: 0.3em 0.6em;
}

.game__start:hover {
  background: #00e200;
}

.game {
  background: #fff;
  position: relative;
  float: left;
  margin-right: 3em;  
  width: 302px;
  height: 295px;

}

.game__btn {
  height: 290px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  position: absolute;
  text-indent: 10000px;
  cursor: pointer;
  opacity: 1 !important;
}

.game__btn__red:active, .game__btn__blue:active, .game__btn__yellow:active, .game__btn__green:active {
  background-color:white;
}



.game__btn__blue {
  background: dodgerblue;
  clip: rect(0px, 150px, 150px, 0px);
  width: 300px;
}

.game__btn__red {
  background: #FF5643;
  clip: rect(0px, 300px, 150px, 150px);
  width: 296px;
  opacity: 1 !important;
}

.game__btn__green {
  background: #BEDE15;
  clip: rect(150px,300px, 300px, 150px);
  width: 296px;
}

.game__btn__yellow {
  background: #FEEF33;
  clip: rect(150px, 150px, 300px, 0px);
  width: 300px;
}

.btn_act {
  background-color:pink;
  
}
button:focus {
    outline: none;
}
.cutout {
  width:50%;
  height:50%;
  background-color:white;
  position:absolute;
  top:25%;
  left:25%;
  border-radius:50%;
  pointer-events:none;
  }
</style>
