<template>
  <div class="bg-slate-600 min-h-screen flex flex-col items-center justify-center">
    <h1 class="text-4xl text-white mb-4">
      reaction 
    </h1>
    <button @click="start" v-if="!gameIsOn" class="bg-blue-500 text-white p-2 rounded-md cursor-pointer">
      Click me to start
    </button>
    <div class="card" v-if="gameIsOn && showCard" @click="clickCard">
      <Card />
    </div>
    <div v-if="showResult" class="flex flex-col items-center justify-center">
      <h2 class="text-white">
        Your reaction time is 0.{{ countTimePassed }} seconds 
      </h2>
      <button @click="start" class="bg-blue-500 text-white p-2 rounded-md cursor-pointer">
        Play again
      </button>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue'
import Card from './components/Card.vue'

const gameIsOn = ref(false)
const countDownFinished = ref(false)
const showCard = ref(false)
const countTimePassed = ref(0)
const interval = ref(null)
const showResult = ref(false)


const start = () => {
  gameIsOn.value = true
  showCard.value = false
  showResult.value = false
  countTimePassed.value = 0
  countDown()
}

const countDown = () => {
  const random = Math.floor(Math.random() * 1000)
  setTimeout(() => {
    console.log(`finished in ${random}ms`)
    countDownFinished.value = true
    showCard.value = true
    startTime()
  },2000 + random)
}

const startTime = () => {
  interval.value = setInterval(() => {
    countTimePassed.value++
    console.log(countTimePassed.value)
  }, 1)
}

const clickCard = () => {
  clearInterval(interval.value)
  showResult.value = true
}

</script>
