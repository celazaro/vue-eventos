<template>
  <div class="container m-5">
    <h1>Eventos</h1>
    <h3>Botones</h3>

    <button
      type="button"
      class="btn btn-primary m-2"
      v-on:click="($event) => hacerClick('Se hizo click en el botón azul')"
    >
      Hacer Click
    </button>

    <button
      type="button"
      class="btn btn-success m-2"
      @click="($event) => hacerClick('Se hizo click en el botón verde')"
    >
      Hacer Click
    </button>
    <hr />
    <h3>Modificadores</h3>

    <button
      type="button"
      class="btn btn-warning m-2"
      @click="($event) => queBotonPresione('Presiono el botón izquierdo')"
    >
      Izquierda
    </button>

    <button
      type="button"
      class="btn btn-info m-2"
      @click.middle="($event) => queBotonPresione('Presiono el botón central')"
    >
      Central
    </button>

    <button
      type="button"
      class="btn btn-danger m-2"
      @click.right.prevent="
        ($event) => queBotonPresione('Presiono el botón derecha')
      "
    >
      Derecha
    </button>

    <hr />
    <h3>
      Reactividad: es cuando los datos que se muestran en la vista cambian
    </h3>

    <p>La variable estática "prueba" vale : {{ prueba }}</p>

    <h4>
      Contador: <strong> {{ contador }} </strong>
    </h4>
    <button
      type="button"
      class="btn btn-sm btn-success m-2"
      @click="($event) => incrementarVariable()"
    >
      Incrementar
    </button>

    <button
      type="button"
      class="btn btn-sm btn-danger m-2"
      @click="($event) => decrementarVariable()"
    >
      Decrementar
    </button>

    <h4>Resultado: <strong> {{ resultado }} </strong> </h4>

    <hr>
    <h3>
      Variables Computadas y Objetos
    </h3>
    <br>
    
    <div class="card" style="width: 18rem;">
      <img :src="bandera" class="card-img-top"  alt="...">
      <div class="card-body">
        <h5 class="card-title"> {{ paisCorregido }} </h5>
        <p class="card-text"> {{ paises[contadorPaises].capital }} </p>
        <p class="card-text"> {{ paises[contadorPaises].moneda }} </p>
        <p class="text-secondary text-center"> {{ contadorPaises + 1 }} de {{ totalPaises}}  </p>
        <button type="button" class="btn btn-sm btn-secondary m-2" @click="($event) => paisAnterior()"  > Anterior </button>
        <button type="button" class="btn btn-sm btn-secondary m-2" @click="($event) => paisSiguiente()" > Siguiente </button>
      </div>
    </div>

  </div>
</template>

<script setup>
const hacerClick = (mensaje) => {
  console.log(mensaje);
};

const queBotonPresione = (mensaje) => {
  console.log(mensaje);
};

const prueba = 2.23;

import { ref, computed } from "vue";

let contador = ref(0);

const incrementarVariable = () => {
  contador.value++;
};

const decrementarVariable = () => {

/*
  if (contador.value <= 0) {
    contador.value = 0;
  } else {
    contador.value--;
  } 
*/ 

  contador.value <= 0 ? (contador.value = 0) : (contador.value--);

};

const resultado = computed(() => {
  /*
  let calculo = parseFloat((contador.value * prueba).toFixed(2));
  return  calculo + 10 ;
  */
  return parseFloat(((prueba * contador.value) + 10).toFixed(2));

});


const paises = [
  {
  bandera: "https://www.banderas-mundo.es/data/flags/w702/ar.webp", 
  nombre: "ARGENTINA",
  capital: "Buenos Aires",
  moneda: "Peso Argentino"
  },
  {
  bandera: "https://www.banderas-mundo.es/data/flags/w702/br.webp", 
  nombre: "BraSIL",
  capital: "Brasilia",
  moneda: "Real"
  },
  {
  bandera: "https://www.banderas-mundo.es/data/flags/w702/cl.webp", 
  nombre: "chile",
  capital: "Santiago de Chile",
  moneda: "Peso Chileno"
  },
  {
  bandera: "https://www.banderas-mundo.es/data/flags/w702/uy.webp", 
  nombre: "UruGUay",
  capital: "Montevideo",
  moneda: "Peso Uruguayo"
  },
  {
  bandera: "https://www.banderas-mundo.es/data/flags/w702/pe.webp", 
  nombre: "perú",
  capital: "Lima",
  moneda: "Sol"
  },
  {
  bandera: "https://www.banderas-mundo.es/data/flags/w702/ve.webp", 
  nombre: "VeneZUELA",
  capital: "Caracas",
  moneda: "Bolívar"
  },
];

const contadorPaises = ref(0);
const totalPaises = paises.length;

const paisSiguiente = () => {
  contadorPaises.value++;
  if (contadorPaises.value >= totalPaises) {
    contadorPaises.value = 0;} 
};

const paisAnterior = () => {
  contadorPaises.value--;
  if (contadorPaises.value < 0) {
    contadorPaises.value = totalPaises - 1;} 
};


const bandera = computed(() => paises[contadorPaises.value].bandera);

const paisCorregido = computed(() => {
  const paisOriginal = paises[contadorPaises.value].nombre.toLowerCase();
  return paisOriginal.substring(0, 1).toUpperCase() + paisOriginal.substring(1);
});

</script>

<style></style>
