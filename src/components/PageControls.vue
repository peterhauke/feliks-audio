<template>
  <div class="control-panel">
    <ButtonLeft>
      <template #icon>
        <LeftArrowIcon />
      </template>
    </ButtonLeft>
    <ButtonPlay :selectedBookNumber="selectedBookNumber" :selectedPageNumber="selectedPageNumber" :selectedPage="selectedPage" :soundId="soundId" :pageId="pageId">
      <template #icon>
        <PlayPauseIcon />
      </template>
    </ButtonPlay>
    <ButtonRight>
      <template #icon>
        <RightArrowIcon />
      </template>
    </ButtonRight>
  </div>
</template>

<style scoped>
.control-panel {
  display: flex;
  flex-wrap: nowrap;
}

</style>

<script setup>
import ButtonLeft from './ButtonLeft.vue'
import ButtonRight from './ButtonRight.vue'
import ButtonPlay from './ButtonPlay.vue'
import LeftArrowIcon from './icons/IconLeftArrow.vue'
import RightArrowIcon from './icons/IconRightArrow.vue'
import PlayPauseIcon from './icons/IconPlayPause.vue'

import { ref } from 'vue'

defineProps({
  selectedPageNumber: Number,
  selectedPage: String,
  selectedBookNumber: Number,
  soundId: String,
  pageId: String
})

</script>