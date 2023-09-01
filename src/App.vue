<script setup>
  import {ref } from "vue";
  import LoadingSpinner from "./components/LoadingSpinner.vue"
  const loading = ref(false)
  const fecha = new Date();
  const fechaact = fecha.getDate() + "-" + (fecha.getMonth() + 1)
  function descarga() {
    loading.value = true;
    console.log("si le diste");
    fetch('http://192.168.12.173:1619/Assist/public/api/assist/report')
      .then(res => {
        if (!res.ok) {
          throw new Error('Network response was not ok');
        }
        return res.blob(); // Convierte la respuesta en un objeto Blob
      })
      .then(blob => {
        const url = window.URL.createObjectURL(blob); // Crea una URL temporal para el Blob
        const a = document.createElement('a'); // Crea un elemento <a> para descargar el archivo
        a.href = url;
        a.download = 'reportedel'+ fechaact + '.xlsx'; // Define el nombre del archivo
        a.click(); // Simula un clic en el enlace
      })
      .catch(error => {
        console.error('Error:', error);
        // Maneja el error si es necesario
      })
      .finally(() => loading.value = false);
  }
  function Justificaciones(){
    loading.value=true
    console.log("si le diste");
    fetch('http://192.168.12.173:1619/Assist/public/api/Monday/justification')
      .then(res => res.json())
      .then(data => alert(data))
      .finally(() =>loading.value = false)
  }
  function ultche(){ 
      loading.value=true
    console.log("si le diste");
    fetch('http://192.168.12.173:1619/Assist/public/api/zkt/Reportcomplete')
      .then(res => res)
      // .then(data => alert(data))
      .finally(() =>loading.value = false)
  }
</script>
<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>Reporte de asistencias</h1>

    <br>
    <div class="d-grid gap-10 col-10 mx-auto">
      <button @click="descarga" type="button" class="btn btn-outline-primary"> Descargar Reporte de asistencias</button>
      <br>
      <button @click="Justificaciones" type="button" class="btn btn-outline-primary" > Replicar Justificaciones</button>
      <br>
      <button @click="ultche" type="button" class="btn btn-outline-primary" > Replicar Ult checadas</button>
    </div>
  </div>
</template>