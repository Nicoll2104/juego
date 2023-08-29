<template>
  <div class="body">
    <div class="contenedor">
      <button v-for="(item, index) in alfa" :key="index" @click="revisar(item)" class="palabras">{{ item }}</button>
    <div class="cuadros">
      <h1 v-if="buscar(item)">{{ item }}</h1>
    </div>
  </div>
  <div>
    <img :src="img1" alt="">
  </div>
</div>
</template>

<script setup>
import{ref,computed} from 'vue'
import img1 from '/src/assets/img1.png'
import img2 from '/src/assets/img1.png'
import img3 from '/src/assets/img1.png'
import img4 from '/src/assets/img1.png'
import img5 from '/src/assets/img1.png'
import img6 from '/src/assets/img1.png'
import img7 from '/src/assets/img1.png'

const alfa = ["A","B","C","D","F","G","H","I","J","K","L","M","N","Ñ","O","P","Q","R","S","T","U","V","W","X","Y","Z"];
const palabra = "ahorcado";
const encotrar = ref([""])

const revisar =(letra) =>{
  if(encotrar.value.includes(letra)) return

  if(palabra.includes(letra.toLowerCase())){
    encotrar.value.push(letra)
    return
  }
}

const buscar = computed(() =>{
  return(letra)=>{
    const bu =encotrar.value.find(e=> String(e)==String)
  }
})

</script>

<style scoped>
.cuadros {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.cuadro {
  width: 30px;
  height: 30px;
  border: 1px solid white;
  margin: 0 5px;
}
</style>
