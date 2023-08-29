<template>
    <div class="body">
      <button v-for="(item,index) in alfa" :key="index" >{{ item }}</button>
    </div>
  </template>
  
  <script setup>
  const alfa =[ "A","B","C","D","F","G","H","I","J","K","L","M","N","Ñ","O","P","Q","R","S","T","U","V","W","X","Y","Z" ]
  </script>
  
  <style scoped>
  
  </style>