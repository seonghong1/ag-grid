<template>
  <span>
    <button @click="buttonClicked">Test</button>
  </span>
</template>

<script setup lang="ts">
const props: any = defineProps({});
const currentValue = props.params.value;
const buttonClicked = () => {
  console.log("first");
  console.log(props.params);
};
</script>

<style scoped></style>
