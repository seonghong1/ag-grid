<template>
  <div :class="isShow ? 'show' : 'hide'">{{ currentValue }}</div>
</template>
<script setup lang="ts">
import { ref } from "vue";
import { dummy_data } from "../../dummy.ts";
const props: any = defineProps({});
const currentValue = props.params.value;

const currentIndex = props.params.node.childIndex;
let isShow = ref(false);
let stopNumber = 0;
const stopNumberArr = [];
const countByDate = {};
const objProps = dummy_data.forEach(({ TRANS_DATE }, index) => {
  if (!countByDate[TRANS_DATE]) {
    stopNumberArr.push(
      (countByDate[TRANS_DATE] = {
        startIndex: index,
      })
    );
  }
});
console.log(stopNumberArr);
for (let i = 0; stopNumberArr.length > i; i++) {
  if (stopNumberArr[i].startIndex === currentIndex) {
    isShow = true;
  }
}
</script>
<style>
.show {
  /* background-color: #fff; */
  position: relative !important;
  z-index: 999 !important;
  height: 2000px !important;
  color: black;
}
.hide {
  font-size: 0;
  background-color: #fff;
}
</style>
