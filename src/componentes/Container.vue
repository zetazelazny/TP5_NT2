<template>
  <section class="src-componentes-container">
    <div id="container">
      <div v-for="i in this.colorCount" :key="i">
        <div
          class="square"
          ref="squares"
          :style="{ 'background-color': colores[i - 1] }"
          @click="chequea"
        ></div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-container",
  props: ['colores','colorHeader','colorCount'],
  mounted() {
            
  },
  data() {
    return {      
    };
  },
  methods: {      
      setAllColorsTo(color) {
          let squares = this.$refs.squares
          squares.map((square) => {
            square.style.backgroundColor = color
        })
      },
    chequea(e){
      const color = e.target.style.backgroundColor
      if (color === this.colorHeader )      {
        this.setAllColorsTo(color)
        this.mensaje = "You Picked Right!"        
        this.$emit("termino", true);      
      }
      else{
         e.target.style.backgroundColor = "#232323";
         this.mensaje = "Try Again!"         
      }
      this.$emit("mensaje-chequeo", this.mensaje);            

    }
  },
  computed: {},
}
</script>

<style scoped lang="css" >
.src-componentes-container {
}
</style>
