<script setup>
import { ref, computed } from "vue";

const name = "Vue dinamico";

const increment = (incre) => {
  console.log("aumentar contador");
  counter.value = counter.value + incre;
};

const arrayNumFav = ref([]);

const counter = ref(0);

const addToArray = (numero) => {
  arrayNumFav.value.push(numero);
};

const disbaleButton = computed(() => {
  return arrayNumFav.value.includes(counter.value);
});

const classCounter = computed(() => {
  if (counter.value > 0) return "green";
  if (counter.value < 0) return "red";
  if (counter.value === 0) return "peru";
});
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :style="{ color: classCounter }">
      {{ counter }}
    </h2>
    <div class="btn-group">
      <button @click="increment(1)" class="btn btn-success">Aumentar</button>
      <button @click="increment(-1)" class="btn btn-danger">Decrementar</button>
      <button @click="increment(-counter)" class="btn btn-secondary">
        Reset
      </button>
      <button
        @click="addToArray(counter)"
        :disabled="disbaleButton"
        class="btn btn-primary"
      >
        Add
      </button>
    </div>
    <ul class="list-group mt-4">
      <li v-for="num in arrayNumFav" :key="num" class="list-group-item">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: red;
}
</style>
