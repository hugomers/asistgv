<script setup>
  import {ref } from "vue";
// const ar = [{
//     "id":1,
//     "sucursal": "SAN PABLO 2",
//     "conexion": "CONECTADO",
//     "registroes": 140
// },
// {
//     "id":3,
//     "sucursal": "SAN PABLO 1",
//     "conexion": "SIN CONEXION",
//     "registroes": 0
// },
// {
//     "id":2,
//     "sucursal": "CORREO 1",
//     "conexion": "CONECTADO",
//     "registroes": 200
// },
// {
//     "id":3,
//     "sucursal": "CORREO 2",
//     "conexion": "SIN CONEXION",
//     "registroes": 0
// }
// ]

defineProps(["sucursal","conexion","registroes"])

</script>

<template>
    <table class="table">
        <thead class="table-dark">
            <tr>
                <th>Sucursal</th>
                <th>Status</th>
                <th>Registros</th>
            </tr>
        </thead>
        <tbody  class="p-3 text-primary-emphasis bg-primary-subtle border border-primary-subtle rounded-3">
            <tr >
                <th >{{ sucursal }}</th>
                <th style="color: red" v-if="conexion == 'SIN CONEXION'" >{{ conexion }}</th>
                <th style="color: black" v-else>{{ conexion }}</th>
                <th > {{ registroes  }}</th>
            </tr>
        </tbody>
    </table>
</template>