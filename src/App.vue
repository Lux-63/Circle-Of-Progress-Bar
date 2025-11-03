<script setup>
import CircumFerence from './components/CircumFerence.vue'
import DashBoard from './components/DashBoard.vue'
import LineBoard from './components/LineBoard.vue'
import { ref } from 'vue'

const isViewCircleBoard = ref(true)
const isViewDashBoard = ref(false)
const isViewLineBoard = ref(false)

function showCircleboard() {
  isViewCircleBoard.value = true
  isViewDashBoard.value = false
  isViewLineBoard.value = false
}
function showDashBoard() {
  isViewCircleBoard.value = false
  isViewDashBoard.value = true
  isViewLineBoard.value = false
}
function showLineBoard() {
  isViewCircleBoard.value = false
  isViewDashBoard.value = false
  isViewLineBoard.value = true
}
</script>

<template>
  <p />
  <header>
    <button @click="showCircleboard">circleboard</button>
    <button @click="showDashBoard">dashBoard</button>
    <button @click="showLineBoard">lineBoard</button>
  </header>
  <p />
  <main>
    <CircumFerence v-if="isViewCircleBoard" />
    <DashBoard v-if="isViewDashBoard" />
    <LineBoard v-if="isViewLineBoard" />
  </main>
</template>

<style></style>
