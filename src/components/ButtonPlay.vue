<template>
  <div class="item book-color"  @click="handleClick(selectedPage, soundId)">
    <p>Old: {{ selectedPageNumber }} X {{ selectedPage }} </p>
    <p>New: {{ soundId }} X {{ pageId }} </p>
    <audio v-bind:id="soundId" v-bind:src="'https://my.anglik.pl/sounds/' + soundId + '.wav'"></audio>
    <img v-bind:src="'https://my.anglik.pl/images/' + selectedPage + '.jpg'">
    <i>
      <slot name="icon"></slot>
    </i>
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

img {
  width: 80%;
  height: auto;
}

</style>

<script setup>
import PageImage from "@/components/PageImage.vue";

defineProps({
  selectedPageNumber: Number,
  selectedPage: String,
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