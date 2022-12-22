<template>

  <section class="src-componentes-juego">
    <br>
    <h2>THE GREAT</h2>
    <h3>Adivina el color RGB:</h3>
    <h1>{{colorStr}}</h1>
    <button class="btn btn-secondary btn-lg m-3" @click="reiniciarJuego()">{{msg}}</button>
    <br>

    <div id="container">
      <button name="btnRGB" class="square" style="background-color: rgb(255, 0, 0);"></button>
      <button name="btnRGB" class="square" style="background-color: rgb(0, 255, 0);"></button>
      <button name="btnRGB" class="square" style="background-color: rgb(0, 0, 255);"></button>
      <button name="btnRGB" class="square" v-if="!modoFacil" style="background-color: rgb(255, 0, 0);"></button>
      <button name="btnRGB" class="square" v-if="!modoFacil" style="background-color: rgb(0, 255, 0);"></button>
      <button name="btnRGB" class="square" v-if="!modoFacil" style="background-color: rgb(0, 0, 255);"></button>
    </div>
    
  </section>
</template>

<script>
  export default  {
    name: 'src-componentes-juego',
    props: [],
    mounted () {
      this.reiniciarJuego()
    },
    data () {
      return {
        colorRgb : {},
        colorStr : {},
        modoFacil : true,
        botones : [],
        msg : ""
      }
    },
    methods: {
      randomRGB()
      {
        let rX = this.getRandomInt(0, 255)
        let gX = this.getRandomInt(0, 255)
        let bX = this.getRandomInt(0, 255)

        return {
          r: rX,
          g: gX,
          b: bX
        }
      },
      cambiarModo()
      {
        this.modoFacil = !this.modoFacil
        this.reiniciarJuego()
      },
      reiniciarJuego()
      {
        this.msg = "A jugar!"
        this.colorRgb = this.randomRGB()
        this.colorStr = "(" + this.colorRgb.r + ", " + this.colorRgb.g + ", " + this.colorRgb.b + ")"
        this.botones = document.getElementsByName("btnRGB")

        let botonesNro = 6
        if(this.modoFacil)
        {
          botonesNro = 3
        }
        
        let botonGanador = this.getRandomInt(0, botonesNro)

        for(var i = 0; i < botonesNro; i++) 
        {
          if(i!=botonGanador)
          {
            this.botones[i].style.backgroundColor = "rgb(" + this.getRandomInt(0, 255) + ", " + this.getRandomInt(0, 255) + ", " + this.getRandomInt(0, 255) + ")"
          }
          else
          {
            this.botones[i].style.backgroundColor = "rgb(" + this.colorRgb.r + ", " + this.colorRgb.g + ", " + this.colorRgb.b + ")"
          }
          
          let colores = this.colorRgb
          this.botones[i].addEventListener("click", function(){
            var clickedColor = this.style.backgroundColor
            console.log(clickedColor)

            var colorGanador = "rgb(" + colores.r + ", " + colores.g + ", " + colores.b + ")"
            console.log(colorGanador)

            if(clickedColor == colorGanador)
            {
              console.log("Ganaste!")
              this.msg = "Felicitaciones! Adivinaste"
            }
          })
        }
      },
      getRandomInt(min, max)
      {
        min = Math.ceil(min);
        max = Math.floor(max);
        return Math.floor(Math.random() * (max - min) + min);
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-juego {
      color: white ;
      background-color: rgb(27, 27, 90);
  }
  .square {
    background-color: rgb(61, 61, 61);
    width: 30%;
    background: rgb(61, 61, 61);
    padding-bottom: 30%;
    float: left;
    margin: 1.66%;
    border-radius: 10%;
    transition: background 0.8s;
    -webkit-transition: background 0.8s;
    -moz-transition: background 0.8s;

  }
  #container 
  {
    margin: 20px auto;
    max-width: 1000px;
  }
</style>
