<template>
  <div>
    <button class="button" :class="{activeButton: isActive}" v-on:click="onClick">{{title}}</button>
  </div>
</template>

<script>
export default {
  name: 'Button',
  props: {
    title: String,
    isActive: Boolean,
    onClick: Function
  }
};
</script>

<style scoped lang="scss">
  .button {
    border: 2px solid black;
    background-color: white;
    color: black;
    border-radius: 10px;
    padding: 7px 12px;
    width: 200px;
    height: 50px;
    font-size: 22px;
    cursor: pointer;

    &:not(.activeButton):hover {
      background-color: lightgray;
    }
  }
  .activeButton {
    background-color: black;
    color: white;
  }
</style>
