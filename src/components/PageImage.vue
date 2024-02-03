<template>
  <div v-bind:class="{ 'item page-color': (selectedPageNumber !== pageNumber), 'item selected': (selectedPageNumber === pageNumber)}" @click="handleClick(pageNumber, soundId)">
<!--    <p><slot></slot></p>-->
<!--    <p v-if="selectedPageNumber === pageNumber">{{ pageNumber }} SEL</p>-->
<!--    <p v-else>{{ pageNumber + '-' +  soundId + '-' + pageId}}</p>-->
    <audio v-bind:id="soundId" v-bind:src="'https://my.anglik.pl/sounds/' + soundId + '.wav'"></audio>
    <img v-bind:src="'https://my.anglik.pl/images/' + pageId + '.jpg'">
  </div>
</template>

<style scoped>
.item {
  flex-grow: 1;
  border: solid 1px black;
  width:20vw;
  min-height:15vh;
  word-wrap: normal;
  font-family: Arial;
  font-size: large;
  font-weight: bold;
  text-align: center;
}

img {
  width: 80%;
  height: auto;
  margin: 10px;
}

.page-color-grey {
  background-color: grey;
  opacity: 60%;
}

.page-color {
  background-color: v-bind('pageBackColor');
  opacity: 60%;
}

.selected {
  background-color: red;
}

</style>

<script setup>
  defineProps({
    pageNumber: Number,
    pageBackColor: String,
    selectedPageNumber: Number,
    selectedBookNumber: Number,
    soundId: String,
    pageId: String
  })

  const emit = defineEmits(['stopAllAudios', 'stopAudios'])

  function handleClick(pageNumber, soundId) {
    // alert(pageNumber + soundId);
    console.log(soundId);
    emit('stopAllAudios', pageNumber);

    const myAudio = document.getElementById(soundId);
    myAudio.currentTime = 0
    myAudio.play();
  }
</script>