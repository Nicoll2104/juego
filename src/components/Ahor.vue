<template>
  <div class="body">
    <div class="contenedor">
      <button v-for="(item, index) in alfa" :key="index" @click="revisar(item)" class="palabras">{{ item }}</button>
      <div class="cuadros">
      <h1 v-for="(letra, index) in palabra" :key="index" @click="comprobar(letra)">{{letra }}</h1>
  </div>
  </div>
  <div>
    <img :src="img[imagen]" alt="">
  </div>
  <div>
    <h1>hola: {{ completado }}</h1>
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
const encontrar = ref([]);
const img =[img1,img2,img3,img4,img5,img6,img7]
const  imagen = ref(0)

const revisar = (letra) => {
  if (encontrar.value.includes(letra)) return;

  if (palabra.includes(letra.toLowerCase())) {
    encontrar.value.push(letra);
    event.target.setAttribute("disabled", "true");
  } else {
    imagen.value += 1;
    event.target.setAttribute("disabled", "true");
  }
};

const comprobar = computed(() =>{
  return (letra) =>{
    const buscar = encontrar.value.find(
    (e) => String(e) === String(letra)
    );
    if(buscar){
      return letra;
    }
    return "";
  };
});

const completado = computed(() =>{
  let confirmacion = false;

  for(const letra of palabra){
    if(!encontrar.value.includes(letra.toUpperCase())){
      confirmacion = false;
      break;
    }

    confirmacion=true
  }

  if(confirmacion===true) return "ganaste"

  return "nada"
});

</script>

<style scoped>
.cuadros {
  display: flex;
  width: 40px;
  height: 40px;
  justify-content: center;
  border: 1px solid rgb(0, 0, 0);
  font-size: x-large;
}
</style>
