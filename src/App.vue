<script setup>
import { ref } from 'vue'
const count = ref(0);
const permission = ref(['create', 'update', 'view', 'delete', 'put', 'destroy']);
const isPending = ref(true);
let status = ref('Pending.....');
let color = ref('skyblue');

function resetCount() {
  count.value = 0;
}
const magicToogle = () => {
  if (isPending.value === true) {
    isPending.value = false;
    status.value = 'Failed.....';
    permission.value[2] = 'posted';
    color.value = 'yellow';
    console.log(status.value);
  } else {
    isPending.value = true;
    status.value = 'Pending.....';
    permission.value.push('viewing')
    color.value = 'green';
    console.log(status.value);
  }
}
</script>

<template>

  <body :style="{backgroundColor: color }">

    <button @click="count++">Count + {{ count }}</button>
    <h1 style="text-align: center;">Current state: {{ count }}</h1>
    <button @click="count--">Count - {{ count }}</button>
    <button @click="resetCount">Reset {{ count }}</button>

    <div class="content" v-for="(item, index) in permission" :key="index">{{ index + 1 }} {{ item }}</div>
    <br>
    <br>
    <p>{{ status }}</p>
    <button @click="magicToogle">Toggle</button>
  </body>
</template>

<style scoped>
.content {
  text-align: center;
}
</style>
