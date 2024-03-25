<template>
  <div v-bind:class="{ 'item page-color': (selectedPageNumber !== pageNumber), 'item selected': (selectedPageNumber === pageNumber)}" @click="handleClick(pageNumber, soundId)">
<!--    <p><slot></slot></p>-->
<!--    <p v-if="selectedPageNumber === pageNumber">{{ pageNumber }} SEL</p>-->
<!--    <p v-else>{{ pageNumber + '-' +  soundId + '-' + pageId}}</p>-->
    <audio v-bind:id="soundId" v-bind:src="'https://my.anglik.pl/sounds/' + soundId + '.wav'"></audio>
<!--    <img v-bind:src="'https://my.anglik.pl/images/' + pageId + '.jpg'">-->
    {{ pageNumber + 1 }}
  </div>
</template>

<style scoped>
.item {
  flex-grow: 1;
  border: solid 1px black;
  width:20vw;
  min-height:12vh;
  word-wrap: normal;
  font-family: Arial;
  text-align: center;
  font-size: 4rem;
  font-weight: bolder;
  display: flex;
  justify-content: center;
  align-items: center;
}

img {
  width: 80%;
  height: auto;
  margin: 10px;
}

h2 {
  font-size: xxx-large;
  font-weight: bolder;
}
.page-color-grey {
  background-color: grey;
  //opacity: 60%;
}

.page-color {
  background-color: v-bind('pageBackColor');
  //opacity: 60%;
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

  const emit = defineEmits(['stopAllAudios', 'stopAudios', 'playAudio'])

  function handleClick(pageNumber, soundId) {
    // alert(pageNumber + soundId);
    console.log(soundId);

    console.log("pressed to play: ", soundId);
    // emit('stopAllAudios', pageNumber);
    emit('playAudio', pageNumber, soundId);

    // const myAudio = document.getElementById(soundId);
    // myAudio.currentTime = 0
    // myAudio.play();
  }
</script>