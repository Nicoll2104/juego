<template>
  <div class="body1">
  <div class="body" v-if="hola===true">
    <div class="div1">
      <div class="sub1">
        <span class="titulo">E</span> <span class="titulo">L</span> <span class="titulo"></span>
        <span class="titulo">A</span> <span class="titulo">H</span> <span class="titulo">O</span>
        <span class="titulo">R</span> <span class="titulo">C</span> <span class="titulo">A</span>
        <span class="titulo">D</span> <span class="titulo">O</span>
      </div>

      <div class="sub3">
          <button @click="showCategoryModal = true">Jugar</button>
        </div>

        <q-dialog v-model="showCategoryModal">
          <q-card>
            <q-card-section>
              <div class="text-h6">Selecciona una categoría</div>
            </q-card-section>
            <q-card-section class="q-pt-none" id="todo">
              <div class="imagen" @click="selectCategory(1)">
                <img src="./assets/colores.png" alt="">
              </div>
              <div class="imagen" @click="selectCategory(2)">
                <img src="./assets/frutas.png" alt="">
              </div>
              <div class="imagen" @click="selectCategory(3)">
                <img src="./assets/animales.png" alt="">
              </div>
              <div class="imagen" @click="selectCategory(4)">
                <img src="./assets/nombres.png" alt="">
              </div>
            </q-card-section>
            <q-card-actions align="right">
              <q-btn flat label="Cerrar" color="primary" v-close-popup @click="showCategoryModal = false" />
            </q-card-actions>
          </q-card>
        </q-dialog>
        <q-dialog v-model="showLevelModal" :persistent="true">
          <q-card>
            <q-card-section>
              <div class="text-h6">Selecciona un nivel</div>
            </q-card-section>
            <q-card-section class="q-pt-none" id="todo">
              <button @click=" hola=false" class="nivel">Facil</button>
              <button @click=" hola=false" class="nivel">Medio</button>
              <button @click=" hola=false" class="nivel">dificil</button>
            </q-card-section>
            <q-card-actions align="right">
              <q-btn flat label="Cerrar" color="primary" v-close-popup @click="showLevelModal = false" />
            </q-card-actions>
          </q-card>
        </q-dialog>
      </div>
      <div class="div2">
      </div>
    </div>
  </div>
  <div v-if="hola===false">
    <div class="contenedor" >
      <button v-for="(item, index) in alfa" :key="index" @click="revisar(item)" class="palabras">{{ item }}</button>
      <div class="cuadros" v-for="l in palabra">
        <p class="cambiar">{{ comprobar(l) }}</p>
      </div>
    </div>
    <div>
      <img :src="img[imagen]" alt="">
    </div>
    <div>
      <h1>estado: {{ completado }}</h1>
    </div>
  </div>
    
</template>

<script setup>
import { ref, computed } from 'vue';
import img1 from '/src/assets/img1.png';
import img2 from '/src/assets/img2.png';
import img3 from '/src/assets/img3.png';
import img4 from '/src/assets/img4.png';
import img5 from '/src/assets/img5.png';
import img6 from '/src/assets/img6.png';
import img7 from '/src/assets/img7.png';

const showCategoryModal = ref(false);
const showLevelModal = ref(false);
const selectedCategory = ref(null);
const alfa = ["A", "B", "C", "D", "F", "G", "H", "I", "J", "K", "L", "M", "N", "Ñ", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"];
const palabra = "koala";
const encontrar = ref([]);
const img = [img1, img2, img3, img4, img5, img6, img7];
const imagen = ref(0);
const hola = ref(true)

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

const selectCategory = (category) => {
  selectedCategory.value = category;
  showCategoryModal.value = false;
  showLevelModal.value = true;
};

const comprobar = computed(() => {
  return (letra) => {
    const buscar = encontrar.value.find(
      (e) => String(e) === String(letra.toUpperCase())
    );
    if (buscar) {
      return letra;
    }
    return "";
  };
});

const completado = computed(() => {
  let confirmacion = false;

  for (const letra of palabra) {
    if (!encontrar.value.includes(letra.toUpperCase())) {
      confirmacion = false;
      break;
    }

    confirmacion = true;
  }

  if (confirmacion === true) return "ganaste";

  return "perdiste";
});
</script>


<style scoped>
  .titulo {
    font-family: 'Black Ops One', cursive;
    display: inline-block;
    border-bottom: 2px solid white;
    padding-bottom: 4px;
  }
  
  .body {
    margin: 0;
    height: 100vh;
    background-image: linear-gradient(to top left, #7364f5, #050b63);
    display: grid;
    grid-template-columns: 50% 50%;
    text-align: center;
  }
  
  .sub1 {
    height: 20%;
    margin-top: 25%;
    font-size: 320%;
  }
  
  .sub2 {
    height: 15%;
  }
  
  span, label {
    color: white;
    font-family: 'Black Ops One', cursive;
    font-size: 180%;
  }
  
  button {
    padding: 2%;
    width: 20%;
    border-radius: 5%;
    border: solid transparent;
  }
  
  a {
    font-size: 200%;
    color: #050b63;
    font-family: 'Black Ops One', cursive;
  }

  #todo{
   margin-top: 20px;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
.imagen {
  width: 500px; 
  border: 1px solid black;
  padding: 10px 0 10px 15px;
}

.cuadros {
  display: flex;
  width: 40px;
  justify-content: center;
  border: 1px solid rgb(0, 0, 0);
  font-size: x-large;
}


</style>
