<template>
  <div class="item book-color-grey">
      <slot></slot>
      <img v-bind:src="'https://my.anglik.pl/b/' + selectedBook.isbn">
<!--      <p>{{ selectedBook.title }}</p>-->
<!--      <p>{{ selectedBook.id}}</p>-->
  </div>
</template>

<style scoped>
.item {
  flex-grow: 1;
  width:30vw;
  border: solid 1px black;
  min-height:16vh;
  font-family: Arial;
  font-size: xx-large;
  font-weight: bolder;
  text-align: center;
}

.book-color-grey {
  background-color: grey;
}

.book-color {
  background-color: v-bind('selectedBook.color');
}
</style>

<script setup>
defineProps({
  selectedBook: {}
})
</script>