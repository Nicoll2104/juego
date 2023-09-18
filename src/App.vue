<template>
  <div class="body1">
    <div class="" v-if="hola === true">
      <h1>{{hola}}</h1>
      <div class="div1">
        <div class="sub1">
          <span class="titulo">E</span> <span class="titulo">L</span>
          <span class="titulo"></span> <span class="titulo">A</span>
          <span class="titulo">H</span> <span class="titulo">O</span>
          <span class="titulo">R</span> <span class="titulo">C</span>
          <span class="titulo">A</span> <span class="titulo">D</span>
          <span class="titulo">O</span>
        </div>
        <button
          class="iniciar"
          @click="
            icon = true;
            formatear();
          "
        >
          jugar
        </button>
        <div class="q-pa-md q-gutter-sm">
          <q-dialog v-model="icon">
            <q-card>
              <q-card-section class="row items-center q-pb-none">
                <div class="text-h6">
                  {{
                    data.categorias === ""
                      ? "Elije la categoría"
                      : "Elije la dificultad"
                  }}
                </div>
                <q-space />
                <q-btn icon="X" flat round dense v-close-popup />
              </q-card-section>
              <q-card-section class="row">
                <div
                  v-for="(item, index) in categorias"
                  :key="index"
                  class="cardCategoria"
                  v-if="cambioPreguntaModal"
                  @click="agregarcate(item.nombre)"
                >
                  <img :src="item.imagen" alt="" class="imgsCategoria" />
                  <h4>{{ item.nombre }}</h4>
                </div>
                <button
                  v-for="(item, i) in dificultades"
                  :key="i"
                  v-else
                  @click="carga(item)"
                >
                  {{ item }}
                </button>
              </q-card-section>
            </q-card>
          </q-dialog>
        </div>
      </div>
    </div>
      <div v-else>
        <div class="contenedor">
          <button
            v-for="(item, index) in alfa"
            :key="index"
            @click="revisar(item)"
            class="palabras"
          >
            {{ item }}
          </button>
          <div class="cuadros" v-for="l in palabra">
            <p class="cambiar">{{ comprobar(l) }}</p>
          </div>
        </div>
        <div>
          <img :src="img[imagen]" alt="" />
          <button @click="volver(completado)"></button>
        </div>
        <div>
          <h1>Estado: {{ completado }}</h1>
        </div>
      </div>
    
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import img1 from "/src/assets/img1.png";
import img2 from "/src/assets/img2.png";
import img3 from "/src/assets/img3.png";
import img4 from "/src/assets/img4.png";
import img5 from "/src/assets/img5.png";
import img6 from "/src/assets/img6.png";
import img7 from "/src/assets/img7.png";
import colores from "/src/assets/colores.png";
import animales from "/src/assets/animales.png";
import frutas from "/src/assets/frutas.png";
import nombres from "/src/assets/nombres.png";

/* const app = ref(true); */
const cambioPreguntaModal = ref(true);
const alfa = [
  "A",
  "B",
  "C",
  "D",
  "F",
  "G",
  "H",
  "I",
  "J",
  "K",
  "L",
  "M",
  "N",
  "Ñ",
  "O",
  "P",
  "Q",
  "R",
  "S",
  "T",
  "U",
  "V",
  "W",
  "X",
  "Y",
  "Z",
];
const baseDatos = {
  colores: {
    Facil: ["Rojo", "Verde", "Azul", "Amarillo", "Blanco"],
    Medio: ["Naranja", "Morado", "Gris", "Rosa", "Negro"],
    Dificil: ["Turquesa", "Magenta", "Cian", "Dorado", "Plateado"],
  },
  frutas: {
    Facil: ["Manzana", "Banana", "Fresa", "Naranja", "Pera"],
    Medio: ["Uva", "Kiwi", "Mango", "Cereza", "Sandía"],
    Dificil: ["Granada", "Pitahaya", "Lichi", "Maracuyá", "Carambola"],
  },
  animales: {
    Facil: ["Perro", "Gato", "Pato", "Conejo", "Tigre"],
    Medio: ["León", "Elefante", "Jirafa", "Cocodrilo", "Hipopótamo"],
    Dificil: ["Oricteropo", "Axolote", "Quokka", "Narval", "Pangolín"],
  },
  nombres: {
    Facil: ["Juan", "Ana", "Carlos", "Luis", "Sofía"],
    Medio: ["Eduardo", "Valentina", "Gabriel", "Isabella", "Mateo"],
    Dificil: ["Sebastián", "Constanza", "Benjamín", "Valeria", "Leonardo"],
  },
};
const palabra = ref([]);
const encontrar = ref([]);
const img = [img1, img2, img3, img4, img5, img6, img7];
const error = ref(0);
const errorDificultad = {
  Facil: 5,
  Medio: 3,
  Dificil: 2,
};
const imagen = ref(0);
const hola = ref(true);
const data = ref({
  categorias: "colores",
  dificultad: "Facil",
});
const numero = () => Math.floor(Math.random() * 3);

const acomodar = () => {
  console.log(data.value);
  const palabras =
    baseDatos[data.value.categorias][data.value.dificultad][numero()];
  const arrpalabras = Array.from(palabras);
  if (palabra.value.length > 0) palabra.value = [];
  for (const letra of arrpalabras) {
    palabra.value.push(letra);
  }
};

const revisar = (letra) => {
  if (palabra.value.includes(letra.toLowerCase())) {
    console.log(
      encontrar.value.includes(letra),
      "data",
      data.value.dificultad !== "dificil"
    );
    if (
      encontrar.value.includes(letra) &&
      data.value.dificultad === "Dificil"
    ) {
      error.value += errorDificultad[data.value.dificultad];
      return;
    }
    encontrar.value.push(letra);
    if (data.value.dificultad !== "Dificil")
      event.target.setAttribute("disabled", "true");
    return;
  }
  error.value += errorDificultad[data.value.dificultad];
  if (data.value.dificultad !== "Dificil")
    event.target.setAttribute("disabled", "true");
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

const volver = (confirmacion) => {
  if (confirmacion === "ganaste" || error.value >= 9) icon.value = true;
  return;
};

const icon = ref(false);

const categorias = [
  {
    nombre: "colores",
    imagen: colores,
  },
  {
    nombre: "frutas",
    imagen: frutas,
  },
  {
    nombre: "animales",
    imagen: animales,
  },
  {
    nombre: "nombres",
    imagen: nombres,
  },
];

const dificultades = ["Facil", "Medio", "Dificil"];

const formatear = () => {
  data.value = {
    categorias: "",
    dificultad: "",
  };
};

const datos = ref([]);
const cargados = ref(false);

const carga = async (item) => {

  encontrar.value = [""];
  icon.value = false;
  cambioPreguntaModal.value = true;
  hola.value = false;
  error.value = 0;
  data.value.dificultad = item;
  /*   app.value = false; */
  cargados.value = true;
  
};

const comenzar = (item) => {
  data.value.dificultad = item;
  /*   app.value = false; */
};

onMounted(() => {});
const agregarcate = (item) => {
  data.value.categorias = item;
  cambioPreguntaModal.value = false;
};
</script>

<style scoped>
.titulo {
  font-family: "Black Ops One", cursive;
  display: inline-block;
  border-bottom: 2px solid white;
  padding-bottom: 4px;
}

.body1 {
  margin: 0;
  height: 100vh;
  background-image: linear-gradient(to top left, #7364f5, #050b63);
  display: grid;
  grid-template-columns: 50% 50%;
  text-align: center;
  align-items: center;
}

.sub1 {
  height: 20%;
  margin-top: 25%;
  font-size: 320%;
}

.sub2 {
  height: 15%;
}

span,
label {
  color: white;
  font-family: "Black Ops One", cursive;
  font-size: 180%;
}

button {
  padding: 2%;
  width: 20%;
  border-radius: 5%;
  border: solid transparent;
  margin: 1% 2%;
  font-size: 150%;
}

a {
  font-size: 200%;
  color: #050b63;
  font-family: "Black Ops One", cursive;
}

.contenedor {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.palabras {
  background-color: #050b63;
  color: white;
  margin: 1%;
  padding: 1% 3%;
  border: 1px solid white;
  cursor: pointer;
}

.cuadros {
  display: flex;
  width: 40px;
  height: 40px;
  justify-content: center;
  align-items: center;
  border: 1px solid rgb(0, 0, 0);
  font-size: x-large;
  margin: 1%;
  background-color: #050b63;
  color: white;
}

img {
  width: 100%;
  max-width: 300px;
  margin: 2% auto;
  display: block;
}

.q-dialog {
  max-width: 400px;
  margin: 0 auto;
}

.q-card-section {
  padding: 1rem;
}

.cardCategoria {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  margin: 1%;
}

.imgsCategoria {
  width: 100px;
  height: 100px;
  margin-bottom: 0.5rem;
}

.cambiar {
  font-size: x-large;
}

h1 {
  font-size: xx-large;
  color: white;
}
</style>
