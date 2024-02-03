<template>
  <div class="control-panel">
    <ButtonLeft>
      <template #icon>
        <LeftArrowIcon />
      </template>
    </ButtonLeft>
    <ButtonSelect :selectedBook="selectedBook"></ButtonSelect>
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
import ButtonSelect from './ButtonSelect.vue'
import LeftArrowIcon from './icons/IconLeftArrow.vue'
import RightArrowIcon from './icons/IconRightArrow.vue'

import { ref } from 'vue'

defineProps({
  startBookNumber: Number,
  selectedBook: {}
})

</script>