<script setup>
import CircumFerence from './components/CircumFerence.vue'
import DashBoard from './components/DashBoard.vue'
import LineBoard from './components/LineBoard.vue'
import { ref } from 'vue'

let currentStateInfo = ref('circleboard')
let currentStateBar = ref(true)

function switchingProgressBar() {
  if (currentStateInfo.value == 'circleboard') {
    currentStateInfo.value = 'dashboard'
    currentStateBar.value = !currentStateBar.value
  } else if (currentStateInfo.value == 'dashboard') {
    currentStateInfo.value = 'circleboard'
    currentStateBar.value = !currentStateBar.value
  }
}
</script>

<template>
  <div>
    <button @click="switchingProgressBar">сейчас {{ currentStateInfo }}</button>
  </div>
  <p />
  <header>
    <div v-if="currentStateBar">
      <circum-ference />
    </div>
    <div v-else="currentStateBar">
      <line-board />
    </div>
  </header>

  <main></main>
</template>

<style>
.wiew-svg {
  position: absolute;
}

.info-position {
  position: absolute;
  width: 110px;
  height: 110px;
  padding-top: 45px;
  left: 60px;
  top: 60px;
  text-align: center;
}
.wiew-error {
  position: absolute;
  width: 110px;
  height: 110px;
  padding-top: 45px;
  left: 5px;
  top: -10px;
}
.wiew-warning {
  position: absolute;
  width: 110px;
  height: 110px;
  padding-top: 45px;
  left: 0px;
  top: -15px;
}

.dots-complette {
  animation: load-complette;
  transition-delay: 3s;
  animation-duration: 3s;
}
@keyframes load-complette {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
.dots-clear {
  animation: precent-clear;
  animation-duration: 5s;
}
@keyframes precent-clear {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}

.dots-one {
  animation-name: animation-one;
  animation-duration: 3s;
}

@keyframes animation-one {
  0% {
    stroke: rgb(255, 0, 0);
  }
  100% {
    stroke: rgb(240, 115, 12);
  }
}
.dots-two {
  animation-name: animation-twenty-five;
  animation-duration: 3s;
  stroke: rgb(240, 115, 12);
}
@keyframes animation-twenty-five {
  from {
    stroke: rgb(240, 115, 12);
  }
  to {
    stroke: rgb(233, 161, 17);
  }
}

.dots-three {
  animation-name: animation-fivty;
  animation-duration: 3s;
  stroke: rgb(233, 161, 17);
}
@keyframes animation-fivty {
  from {
    stroke: rgb(233, 161, 17);
  }
  to {
    stroke: rgb(17, 150, 233);
  }
}

.dots-four {
  animation-name: animation-seventy-five;
  animation-duration: 3s;
  stroke: rgb(17, 150, 233);
}
@keyframes animation-seventy-five {
  from {
    stroke: rgb(17, 150, 233);
  }
  to {
    stroke: rgb(17, 42, 233);
  }
}

.dots-five {
  animation-name: animation-one-hundred;
  animation-duration: 3s;
  stroke: rgb(17, 42, 233);
}
@keyframes animation-one-hundred {
  from {
    stroke: rgb(17, 42, 233);
  }
  to {
    stroke: rgb(28, 233, 17);
  }
}

.dots-warning {
  animation-name: animation-warning;
  animation-duration: 3s;
  stroke: rgb(233, 175, 17);
}
@keyframes animation-warning {
  from {
    /* stroke: rgb(17, 42, 233); */
  }
  to {
    stroke: rgb(233, 175, 17);
  }
}

.dots-error {
  animation-name: animation-error;
  animation-duration: 3s;
  stroke: rgb(233, 17, 17);
}
@keyframes animation-error {
  from {
    /* stroke: rgb(17, 42, 233); */
  }
  to {
    stroke: rgb(233, 17, 17);
  }
}
</style>
