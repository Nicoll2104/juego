<template>
  <div class="body1">
    <div class="" v-if="hola === true">
      <div class="div1">
        <img class="logo" src="https://tomplay.com/storage/section-pages/November2022/CzKiXyiZ7kBUBY2iANmG.png" alt="">
        <div class="sub1">
          <span class="titulo">E</span> <span class="titulo">L</span> <span class="titulo"></span> <span class="titulo">A</span> <span class="titulo">H</span> <span class="titulo">O</span> <span class="titulo">R</span> <span class="titulo">C</span> <span class="titulo">A</span> <span class="titulo">D</span> <span class="titulo">O</span>
        </div>
        <button type="button" class="btn btn-warning"
          @click="
            icon = true;
            formatear();
          "
        >jugar
        </button>
      </div>
    </div>
      <div class="div2" v-else>
        <div class="imagen">
          <img class="avances" :src="completado ==='ganaste' ? ganaste : imagen<8 ? img[imagen] : perdiste" alt="" />
        </div>
          <div class="solo">
            <div class="cuadros" v-for="letra in palabra">
            <p class="cambiar">{{comprobar(letra.toLowerCase()) }}</p>
          </div>
          </div>
          <div class="contenedor">
            <div class="letras">
              <button
            v-for="(item, index) in alfa"
            :key="index"
            @click="revisar(item)"
            :disabled="imagen > 8 || completado ==='ganaste'"  class="palabras"
          >
            {{ item }}
          </button>
            </div>
          <div>
          <button class="volver" @click="volver(completado); icon = true;">volver</button>
        </div>
        </div>
      </div>
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
                <q-btn class="cerrar" icon="X" flat round dense v-close-popup />
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
                <button class="botones"
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
</template>

<script setup>
import { ref, computed } from "vue";
import img1 from "/src/assets/img1.png";
import img2 from "/src/assets/img2.png";
import img3 from "/src/assets/img3.png";
import img4 from "/src/assets/img4.png";
import img5 from "/src/assets/img5.png";
import img6 from "/src/assets/img6.png";
import img7 from "/src/assets/img7.png";
import img8 from "/src/assets/img8.png";
import img9 from "/src/assets/img9.png";
import colores from "/src/assets/colores.png";
import animales from "/src/assets/animales.png";
import frutas from "/src/assets/frutas.png";
import nombres from "/src/assets/nombres.png";
import ganaste from "/src/assets/ganaste.png";
import perdiste from "/src/assets/perdiste.png";
const cambioPreguntaModal = ref(true);
const alfa = [
  "A",
  "B",
  "C",
  "D",
  "E",
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
    Facil: ["rojo", "verde", "azul", "amarillo", "blanco"],
    Medio: ["naranja", "morado", "gris", "rosado", "negro"],
    Dificil: ["turquesa", "magenta", "cian", "dorado", "plateado"],
  },
  frutas: {
    Facil: ["manzana", "banana", "fresa", "naranja", "pera"],
    Medio: ["uva", "kiwi", "mango", "cereza", "sandia"],
    Dificil: ["granada", "pitahaya", "lichi", "maracuya", "carambola"],
  },
  animales: {
    Facil: ["perro", "gato", "pato", "conejo", "tigre"],
    Medio: ["león", "elefante", "jirafa", "cocodrilo", "hipopotamo"],
    Dificil: ["oricteropo", "axolote", "quokka", "narval", "pangolin"],
  },
  nombres: {
    Facil: ["juan", "ana", "carlos", "luis", "sofia"],
    Medio: ["eduardo", "valentina", "gabriel", "isabella", "mateo"],
    Dificil: ["sebastian", "constanza", "benjamin", "valeria", "leonardo"],
  },
};
const palabra = ref([]);
const encontrar = ref([]);
const img = [img1, img2, img3, img4, img5, img6, img7, img8, img9];
const error = ref(0);
const errorDificultad = {
  Facil: 1,
  Medio: 2,
  Dificil: 3,
};
const imagen = ref(0);
const hola = ref(true);
const data = ref({
  categorias: "colores",
  dificultad: "Facil",
});
const numero = () => Math.floor(Math.random() * 3);

const acomodar = () => {
  imagen.value = 0;
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
      imagen.value += errorDificultad[data.value.dificultad];
      return;
    }
    encontrar.value.push(letra);
    if (data.value.dificultad !== "Dificil")
      event.target.setAttribute("disabled", "true");
    return;
  }
  imagen.value += errorDificultad[data.value.dificultad];
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
  for (const letra of palabra.value) {
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
  if (confirmacion === "ganaste" || error.value >= 9) {
    icon.value = true;
    imagen.value = 0;
    encontrar.value = [];
    error.value = 0;
    palabra.value = [];
  }
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
  cargados.value = true;
  
  acomodar();
};

const agregarcate = (item) => {
  data.value.categorias = item;
  cambioPreguntaModal.value = false;
};
</script>

<style scoped>

.titulo {
  font-family: Georgia, 'Times New Roman', Times, serif;
  display: inline-block;
  border-bottom: 2px solid #FFF800;
  padding-bottom: 4px;
}

.body1 {
  margin: 0;
  height: 100vh;
  background-image: linear-gradient(to top left, #7364f5, #050b63);
  text-align: center;
  align-items: center;
  background-size: cover; 
  background-attachment: fixed;
}

.sub1 {
  text-align: center;
  font-size: 320%;
}

span,
label {
  
  color: #FFF800;
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

img {
  width: 100%;
  max-width: 300px;
}

.logo{
  height: 330px;
  width: 100%;
  max-width: 300px;
  margin-top: 6%;
}

.cardCategoria {
  display: flex;
  flex-direction: column-reverse;
  align-items: center;
  cursor: pointer;
  margin: 1%;
}
.imgsCategoria {
  width: 200px;
  height: 300px;
  margin-bottom: 0.5rem;
  background-color: #8fe3ff;
  width: 100%;
  border-radius: 100%;
}

.cambiar {
  font-size: x-large;
}

h1 {
  font-size: xx-large;
  color: white;
}
.btn.btn-warning{
  padding: 0.5%;
  font-family: Georgia, 'Times New Roman', Times, serif;
  background-color: #8fe3ff;
  color: #050b63;
}
.q-card{
  width: 100%;
  border: solid;
  flex-direction:column-reverse;
  background-color: #FEC8D8;
  color: #050b63;
  font-family: Georgia, 'Times New Roman', Times, serif;
}
.text-h6{
  color: #050b63;
  font-weight: 900;
}
.botones{
 display: flex;
 padding: 1%;
 width: 25%;
 text-align: center;
 background-color: #050b63;
 color: #FFF800;
}
.row.items-center.q-pb-none{
  display: flex;
  flex-direction: column;
}
.cerrar{
  margin-top: -8%;
  margin-left: 80%;
}
.avances{
  max-width: 86%;
  margin-top: 4%;
  border: solid 10px #ffc0dd;
}
.div2{
  display: flex;
}
.imagen{
  width: 40%;
}
.solo{
  width: 10%;
  margin-top: 5%;
}
.contenedor{
  display: flex;
  flex-direction:column;
  margin-left: 7%;
}
.palabras{padding: 0.%;
  background-color: #C4FAF8;
  border: solid 5px #050b63;
  color: #050b63;
  font-weight: 900;
  font-family: Georgia, 'Times New Roman', Times, serif;
}
.letras{
  margin-left: -4%;
}
.volver{
  background-color: #050b63;
  border: solid 5px #FFF800;
  color: #FFF800;
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-weight: 900;
}

@media(max-width: 2000px) {
  .cuadros {
  margin: 10%;
  width: 50%;
  height: 10%;
  justify-content: center;
  align-items: center;
  border: 3px solid #FFF800;
  background-color: #050b63;
  color: #FFF800;
  font-family: Georgia, 'Times New Roman', Times, serif;
}
}


@media (min-width: 350px) and (max-width: 1200px) {
  .body1 {
    height: 190vh;
  }

  .sub1 {
    font-size: 250%;
  }

  button {
    width: 30%;
  }

  .contenedor {
    margin-left: 2%;
  }

  .palabras {
    padding: 1%;
  }

  .letras {
    margin-left: 0;
  }

  .volver {
    padding: 1% 5%;
  }

  .logo {
    height: 250px;
    margin-top: 3%;
  }

  .avances {
    max-width: 90%;
    margin-top: 2%;
  }

  .div2 {
    flex-direction: column;
    
  }

  .imagen {
    width: 80%;
    margin: 0 auto;
  }

  .solo {
    width: 20%;
    margin-top: 2%;
  }

  .contenedor {
    margin-left: 2%;
  }

  .cerrar {
    margin-top: -10%;
    margin-left: 70%;
  }

}



</style>