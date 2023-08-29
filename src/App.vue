<template>
<div class="body">
  

  <div class="div1">
    <div class="sub1">
      <span class="titulo">E</span> <span class="titulo">L</span> <span class="titulo"></span> <span class="titulo">A</span> <span class="titulo">H</span> <span class="titulo">O</span> <span class="titulo">R</span> <span class="titulo">C</span> <span class="titulo">A</span> <span class="titulo">D</span> <span class="titulo">O</span>
    </div>
     <div class="sub2"><label>
      <input
        type="radio"
        name="opciones"
        value="opcion1"
        v-model="selectedOption"
      />
      Fácil
    </label>
    <label>
      <input
        type="radio"
        name="opciones"
        value="opcion2"
        v-model="selectedOption"
      />
      Madio
    </label>
    <label>
      <input
        type="radio"
        name="opciones"
        value="opcion3"
        v-model="selectedOption"
      />
      Difícil
    </label>
  </div>
   <div class="sub3">
    <button><a href="../ahor.html">Jugar</a></button>
  </div>
  </div>
  <div class="div2">
    <img src="https://play-lh.googleusercontent.com/0jPtxKhDh0UqcKOBf8wEXoQqwcuKvCWXGZabbqj5v9qQtgKyxIlDW4qxgPhmI5h0Hoc=s128-h480-rw" alt="">
  </div>
 
 
  


<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Black+Ops+One&display=swap" rel="stylesheet">
  

</div>
</template>

<script setup>

</script>

<style scoped>

.titulo{
  font-family: 'Black Ops One', cursive;
  display: inline-block;
  border-bottom: 2px solid white; /* Grosor y color de la línea */
  padding-bottom: 4px; 

}
.body{
  margin: 0;
  height: 100vh;
  background-image: linear-gradient(to top left, #7364f5, #050b63);
  display: grid;
  grid-template-columns: 50% 50%;
  text-align: center;
}
.sub1{
  height: 20%;
  margin-top: 25%;
  font-size: 320%;
}
.sub2{
  height:15%;
}

span, label{
  color: white;
  font-family: 'Black Ops One', cursive;
  font-size: 180%;
}

button{
padding: 2%;
width: 20%;
border-radius: 5%;
border: solid transparent;
}
a{
  font-size: 200%;
  color: #050b63;
  font-family: 'Black Ops One', cursive;
}
</style>
