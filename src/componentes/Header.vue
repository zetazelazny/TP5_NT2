<template >
  <section class="src-componentes-header">
    <div id="header" :style="{ 'background-color': termino?pickedColor:'steelblue'}">
      <h1>
        The Great <br />
        <span id="colorDisplay"> {{ pickedColor }} </span>                
        <br />        
        Guessing Game
      </h1>            
      <Navigator :termino="termino" :mensaje="mensajeChequeo" @is-hard-navigator="isHard=$event" @restart="this.restart" @color-count="colorCount=$event"/>
      <Container :color-count="colorCount" :colores="colors" :colorHeader="pickedColor" @mensaje-chequeo="mensajeChequeo=$event" @termino="termino=$event"/>     
      
      
    </div>
     
  </section>
</template>

<script >
import Navigator from './Navigator.vue'
import Container from './Container.vue'
export default {
  name: "src-componentes-header",
  components: {
    Navigator,
    Container
  },
  props: [],
  mounted() {    
    this.restart();
  },
  data() {
    return {
      pickedColor: "(256,256,256)",      
      colorCount: 6,
      colors: [],   
      isHard:true,     
      mensajeChequeo:'',
      termino : false
      
    };
  },
  methods: {
    PickColor() {      
      let quantity;    
      if (this.isHard) {
        quantity = 6;
      } else {
        quantity = 3;
      }
      return Math.floor(Math.random() * quantity);
    },
    randomInt() {
      return Math.floor(Math.random() * 256);
    },
    createRandomStringColor() {      
      var newColor =
        "rgb(" +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ")";
      return newColor;
    },
    createNewColors(numbers) {      
      var arr = [];
      for (var i = 0; i < numbers; i++) {
        arr.push(this.createRandomStringColor());
      }
      return arr;
    },
    restart() {      
      this.colors = this.createNewColors(this.colorCount);      
      this.pickedColor = this.colors[this.PickColor()];
      this.mensajeChequeo=''
      this.termino = false
    },
  },
  computed: {},
};
</script>

<style scoped lang="css" >
.src-componentes-fondo {
}

</style>


