<template>
  <div class="item" @click="$parent.$emit('increaseBy', 1)">
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
  display: flex;
  justify-content: center;
}
</style>

<script>
</script>