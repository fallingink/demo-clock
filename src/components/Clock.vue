<script setup lang="ts">
import { onMounted, ref, Ref } from "vue";

const scale: Ref<HTMLDivElement | null> = ref(null);
const secondHand: Ref<HTMLDivElement | null> = ref(null);
const minuteHand: Ref<HTMLDivElement | null> = ref(null);
const hourHand: Ref<HTMLDivElement | null> = ref(null);
// hourHand.value?.style.transform = `rotate(30deg)`;
// const clock:Ref<HTMLDivElement | null> = ref(null);


// 刻度呈现
function scaleShow(scaleElement: HTMLDivElement): void {
  for (let i: number = 1; i < 6; i++) {
    const copyScaleEl = scaleElement.cloneNode(true) as HTMLDivElement;
    copyScaleEl.style.transform = `rotate(${30 * i}deg)`;
    scaleElement.parentNode?.appendChild(copyScaleEl);
  }
}

// 秒针跑动
function secondHandRun(secondHandElement: HTMLDivElement): void {
  setInterval(() => {
    const date = new Date();
    const second = date.getSeconds();
    secondHandElement.style.transform = `rotate(${6 * second - 90}deg)`;
  }, 1000);
}

//分针跑动
function minuteHandRun(minuteHandElement: HTMLDivElement): void {
  setInterval(() => {
    const date = new Date();
    const minute = date.getMinutes();
    minuteHandElement.style.transform = `rotate(${6 * minute - 90}deg)`;
  }, 1000);
}

// 时针跑动
function hourHandRun(hourHandElement: HTMLDivElement): void {
  setInterval(() => {
    const date = new Date();
    const hour = date.getHours();
    hourHandElement.style.transform = `rotate(${30 * hour - 90}deg)`;
  }, 1000);
}

onMounted((): void => {
  const scaleElement = scale.value as HTMLDivElement;
  const secondHandElement = secondHand.value as HTMLDivElement;
  const minuteHandElement = minuteHand.value as HTMLDivElement;
  const hourHandElement = hourHand.value as HTMLDivElement;
  scaleShow(scaleElement);
  secondHandRun(secondHandElement);
  minuteHandRun(minuteHandElement);
  hourHandRun(hourHandElement);
});
</script>

<template>
  <div ref="clock" :class="[$style.clock]">
    <div ref="scale" :class="[$style.scale]"></div>
    <div :class="$style['clock-point']">
      <div ref="secondHand" :class="[$style['second-hand'],$style['hand']]"></div>
      <div ref="minuteHand" :class="[$style['minute-hand'],$style['hand']]" ></div>
      <div ref="hourHand" :class="[$style['hour-hand'],$style['hand']]" ></div>
    </div>
  </div>
</template>

<style module>
body{
  background-color: #696767;
  position: relative;
  z-index: -999;
}
.clock {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
  width: 200px;
  border-radius: 50%;
  border: 2px solid #fff;
  position: relative;
}

.scale {
  width: 100%;
  box-sizing: border-box;
  height: 2px;
  border-left: 8px solid #fff;
  border-right: 8px solid #fff;
  position: absolute;
}



.hand{
  position: absolute;
  top:0;
  left:0;
}

.second-hand {
  width: 90px;
  height: 2px;
  background-color: #fff;
  transform-origin: 1px 1px 0;
  z-index: -3;
}
.minute-hand{
  width: 70px;
  height: 4px;
  top: -1px;
  background-color: #85f410;
  transform-origin: 1px 2px 0;
  z-index: -2;
}
.hour-hand{
  width: 50px;
  height: 6px;
  top: -2px;
  background-color: #35bfff;
  transform-origin: 1px 3px 0;
  z-index: -1;
}
.clock-point {
  width: 2px;
  height: 2px;
  border-radius: 50%;
  background-color: #41b883;
  border: 4px solid #41b883;
  position: relative;
}
</style>
