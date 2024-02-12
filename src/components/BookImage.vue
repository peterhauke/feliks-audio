<template>
  <div v-bind:class="{ 'item book-color-grey': (selectedBookNumber !== bookNumber), 'item selected': (selectedBookNumber === bookNumber)}" @click="$emit('selectCurrent', bookNumber)">
<!--    <p><slot></slot></p>-->
<!--    <p v-if="selectedBookNumber === bookNumber">{{ bookNumber }} SEL</p>-->
<!--    <p v-else>{{ bookNumber }}</p>-->
    <img v-bind:src="'https://my.anglik.pl/images/' + bookImage">

  </div>
</template>

<style scoped>
.item {
  flex-grow: 1;
  border: solid 1px black;
  width:20vw;
  min-height:13vh;
  word-wrap: normal;
  font-family: Arial;
  font-size: large;
  font-weight: bold;
  text-align: center;
}

img {
  width: 80%;
  height: auto;
}

.book-color {
  background-color: v-bind('bookBackColor');
}

.book-color-grey {
  background-color: grey;
  opacity: 60%;
}

.selected {
  background-color: yellow;
}
</style>

<script setup>
  defineProps({
    bookNumber: Number,
    bookBackColor: String,
    selectedBookNumber: Number,
    bookImage: String
  })
</script>