<script lang="ts" setup>
import {ref, Ref} from 'vue'

let second: Ref<number> = ref(60)
let minutes: Ref<number> = ref(1)
let hours: Ref<number> = ref(1)
let ifFirst: Ref<boolean> = ref(false)
const times = ref(Date.now())


const handelClickStart: (e: any) => void = (e) => {
  new Notification('倒计时', {body: '倒计时开始'})
  times.value = Date.now();
  ifFirst.value = true;
  let time = second.value * 1000 + minutes.value * 60000 + hours.value * 3600000;
  times.value += time;
  handelButton(e)
}

const handelClickEnd: (e: any) => void = (e) => {
  times.value = Date.now()
  handelButton(e)
}

const countDownEnd: () => void = () => {
  if (ifFirst.value) {
    new Notification('倒计时', {body: '倒计时结束'})
  }
}

const handelButton: (e: any) => void = (e) => {
  let target = e.target
  if (target.nodeName === 'BUTTON' || target.nodeName === 'SPAN') {
    target.parentNode.blur()
  }
  target.blur()
}

</script>

<template>
  <el-button :plain="true" type="success" @click="handelClickStart">开始倒计时</el-button>
  <el-button :plain="true" type="warning" @click="handelClickEnd">关闭倒计时</el-button>
  <el-countdown :value="times" style="margin-top: 30px" @finish="countDownEnd"/>
</template>

<style>

@font-face {
  font-family: 'LXGWWenKaiGBScreen';
  src: url("font/LXGWWenKaiGBScreen.ttf")
}

* {
  font-family: 'LXGWWenKaiGBScreen', serif;
}
</style>
