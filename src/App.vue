<script setup>
import CircumFerence from './components/icons/CircumFerence.vue'
import { ref, onMounted } from 'vue'

let lengthCircumference = 0
let mistakeLoad = false // needed to give an error or warning.
let progressLoad = 0 // how many were loaded.
let StartLoading = 0 // to start painting the circle with red color.
let circleBar = ref(null)
let wiewStatusLoad = ref(0)
let progressBarLoad = ref(678)
let radiusCircle = 0
let startInterval = null
let colorBar = '#00cc00'
// let lengthCircumference = 2 * 3.14 * Number(circleBar.value.getAttribute('r'))
onMounted(() => {
  lengthCircumference = 2 * 3.14 * Number(circleBar.value.getAttribute('r'))
  radiusCircle = Number(circleBar.value.getAttribute('r'))
  // progressBarLoad = ref(0)
  console.log(lengthCircumference, radiusCircle)
})

/*

function stepProgress() {
    console.log(mistakeLoad);
    if(StartLoading == 0){
        circleBar.style.stroke = "rgb(255, 0, 0)";
    }
    StartLoading = 1;
    if (progressLoad <= 100  && mistakeLoad === false) {
        // progressLoad += 0.03;
        progressLoad += 0.1;
        progressBarLoad = circumference * ((100 - progressLoad) / 100);
        wiewPrecentLoad.innerHTML = Math.round(progressLoad);
        drawColorBar();
        console.log(progressLoad);
    } else {
        stopAutoLoadBar();
        console.log("loading stopped");
    }
};
 */

function stepProgress() {
  // console.log(mistakeLoad)
  if (StartLoading == 0) {
    //if there is no check, then every time the download continues, a red color will appear.
    colorBar = 'rgb(255, 0, 0)'
    circleBar.value.style.stroke = colorBar
  }
  StartLoading = 1
  if (progressLoad < 100 && mistakeLoad === false) {
    // progressLoad += 0.03;
    progressLoad += 0.1
    progressBarLoad.value = lengthCircumference * ((100 - progressLoad) / 100)

    wiewStatusLoad.value = Math.round(progressLoad)
    drawColorBar(progressLoad)
    console.log('info %', progressBarLoad.value, progressLoad)
  } else {
    // stopAutoLoadBar()
    // console.log('loading stopped')
  }
  console.log()
}
function drawColorBar(n) {
  let progressLoad = n

  console.log('старт рисования')
  if (Math.round(progressLoad) >= 20 && progressLoad < 25) {
    console.log('сработало')
    colorBar = '#cb0a0a'
    circleBar.value.classList.add('dots-one')
    circleBar.value.style.stroke = 'rgb(240, 115, 12)'
    colorBar = 'rgb(240, 115, 12)'
  } else if (Math.round(progressLoad) >= 45 && progressLoad < 50) {
    circleBar.value.style.stroke = 'rgb(240, 115, 12)'
    circleBar.value.classList.remove('dots-one')
    circleBar.value.classList.add('dots-two')
    circleBar.value.style.stroke = 'rgb(233, 161, 17)'
    colorBar = 'rgb(233, 161, 17)'
  } else if (Math.round(progressLoad) >= 70 && progressLoad < 75) {
    circleBar.value.style.stroke = 'rgb(233, 161, 17)'
    circleBar.value.classList.remove('dots-two')
    circleBar.value.classList.add('dots-three')
    circleBar.value.style.stroke = 'rgb(17, 150, 233)'
    colorBar = 'rgb(17, 150, 233)'
  } else if (Math.round(progressLoad) >= 85 && progressLoad < 100) {
    circleBar.value.style.stroke = 'rgb(17, 150, 233)'
    circleBar.value.classList.remove('dots-three')
    circleBar.value.classList.add('dots-four')
    circleBar.value.style.stroke = 'rgb(17, 42, 233)'
    colorBar = 'rgb(17, 42, 233)'
  } else if (Math.round(progressLoad) == 100) {
    circleBar.value.style.stroke = 'rgb(17, 42, 233)'
    circleBar.value.classList.remove('dots-four')
    circleBar.value.classList.add('dots-five')
    circleBar.value.style.stroke = 'rgb(28, 233, 17)'
    colorBar = 'rgb(28, 233, 17)'
    // wiewPrecentLoad.className += 'dots-clear'
    // infoPosition += 'dots-clear'
    // wiewStatusLoad.insertAdjacentHTML(
    //   'afterbegin',
    //   '<svg class="js-load-complete dots-complette" y="0px" style="enable-background:new 0 0 512.003 512.003;" xml:space="preserve" x="0px" viewBox="-400 100 1212.003 512.003"><g><g><path style="fill:rgb(28, 233, 17)" d="M507.291,57.14c-5.605-4.851-14.094-4.204-18.998,1.455L174.383,424.81l-151.39-151.39 c-5.255-5.255-13.797-5.255-19.052,0c-5.255,5.255-5.255,13.797,0,19.052l161.684,161.684c2.533,2.506,5.982,3.934,9.539,3.934 c0.162,0,0.35,0,0.539,0.027c3.746-0.162,7.276-1.886,9.701-4.716L508.773,76.138C513.597,70.479,512.95,61.99,507.291,57.14z"></path></g></g></svg>',
    // )
  }
  circleBar.value.style.stroke = colorBar
  // circleBar.value.style.stroke = 'rgb(17, 42, 233)'
  circleBar.value.style.strokeDashoffset = `${progressBarLoad.value}`
  console.log(lengthCircumference, progressLoad, progressBarLoad.value)
}
function checkButton() {
  progressBarLoad.value = lengthCircumference * ((100 - progressLoad) / 100)
  // let lengthCircumference = 2 * 3.14 * Number(circleBar.value.getAttribute('r'))
  console.log(
    progressLoad,
    progressBarLoad.value,
    'check r',
    Number(circleBar.value.getAttribute('r')),
  )
}

function startAutoLoadBar() {
  startInterval = setInterval(() => {
    circleBar.value.style.stroke = 'rgb(255, 0, 0)'
    stepProgress()
  }, 10)
}

function stopAutoLoadBar() {
  setTimeout(clearInterval(startInterval))
}
</script>

<template>
  <header>
    <div>
      <button @click="startAutoLoadBar()">autostart</button>
      <button @click="stopAutoLoadBar()">autostop</button>
      <button @click="checkButton()">testing</button>
      <button @click="stepProgress()">step</button>
    </div>
    <div>
      <svg
        class="loading-circumference"
        width="236"
        height="236"
        viewBox="-29.5 -29.5 295 295"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        style="transform: rotate(-90deg)"
      >
        <circle
          class="circle-bar-size js-load-bar"
          r="127"
          cx="118"
          cy="118"
          fill="transparent"
          stroke="#e0e0e0"
          stroke-width="17"
        ></circle>
        <circle
          ref="circleBar"
          class="circle-bar-size"
          r="127"
          cx="118"
          cy="118"
          fill="transparent"
          stroke="rgb(224, 224, 224)"
          stroke-width="17"
          stroke-linecap="round"
          stroke-dasharray="800"
        ></circle>
      </svg>
    </div>
    <div>
      {{ wiewStatusLoad }}
    </div>
  </header>

  <main></main>
</template>

<style>
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
