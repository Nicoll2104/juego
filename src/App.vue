<template>
  <div class="body">
    <div class="div1">
      <div class="sub1">
        <span class="titulo">E</span> <span class="titulo">L</span> <span class="titulo"></span>
        <span class="titulo">A</span> <span class="titulo">H</span> <span class="titulo">O</span>
        <span class="titulo">R</span> <span class="titulo">C</span> <span class="titulo">A</span>
        <span class="titulo">D</span> <span class="titulo">O</span>
      </div>

      <div class="sub3">
        <button @click="showModal = true">Jugar</button>
      </div>
      <q-dialog v-model="showModal">
        <q-card>
          <q-card-section>
            <div class="text-h6">categorías</div>
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
            <q-btn flat label="Cerrar" color="primary" v-close-popup @click="showModal = false" />
          </q-card-actions>
        </q-card>
      </q-dialog>
    </div>
    <div class="div2">
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const showModal = ref(false);
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

</style>
