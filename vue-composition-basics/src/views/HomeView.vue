<template>
  <div class="home">
    <h1>{{ appTitle }}</h1>
    <p>Author: {{ appInfo.author }}</p>
    <h2>The {{ counterTitle }}:</h2>
    <div class="counter">
      <button @click="decreaseCounter">-</button>
      <p>{{ counter }}</p>
      <button @click="increaseCounter">+</button>
    </div>
    <div class="edit">
      <h4>Edit Counter Title</h4>
      <input v-model="counterTitle" />
    </div>
    <h2>The {{ counterData.title }}:</h2>
    <div class="counter">
      <button @click="decreaseCount(2, $event)">--</button>

      <button @click="decreaseCount(1, $event)">-</button>
      <p>{{ counterData.count }}</p>
      <button @click="increaseCount()">+</button>
      <button @click="increaseCount(2)">++</button>
      <p>This count is {{ oddOrEven }}</p>
    </div>
    <div class="edit">
      <h4>Edit Counter Title</h4>
      <input v-model="counterData.title" />
    </div>
    <div class="button-container">
      <div class="triangle-button">My Button</div>
      <div class="triangle-button">Button2</div>
      <div class="triangle-button">Button2</div>
    </div>
  </div>
</template>

<script setup>
import { computed, reactive, ref, watch } from 'vue'
// non reactive data
const appTitle = 'My amazing Conters'
const appInfo = { author: 'uday' }
// ractive data
const counter = ref(0),
  counterTitle = ref()
watch(counter, (nv, ov) => {
  console.log(nv, ov)
  if (nv === 10) alert(`way to go you reached 10 on ${counterTitle.value}`)
})
function increaseCounter() {
  counter.value++
}
// const increaseCounter = () => {
//   counter.value++
// }
const decreaseCounter = () => {
  counter.value--
}

// counter react object
const counterData = reactive({
  count: 0,
  title: ''
})

watch(
  () => counterData.count,
  (nv, ov) => {
    console.log(nv, ov, counterData.title)
    if (nv === 20) {
      alert(`way to go you have reached 10 on ${counterData.title}`)
    }
  }
)

function increaseCount(amount) {
  console.log(amount)
  counterData.count += amount || 1
}
// const increaseCounter = () => {
//   counter.value++
// }
const decreaseCount = (amount, e) => {
  console.log(e)
  counterData.count -= amount || 1
}

const oddOrEven = computed(() => {
  if (counterData.count % 2 === 0) return 'Even'
  return 'Odd'
})
</script>
<!--
<script>
import { ref } from 'vue'
export default {
  setup() {
    const counter = ref(0)
    function increaseCounter() {
      counter.value++
    }
    // const increaseCounter = () => {
    //   counter.value++
    // }
    const decreaseCounter = () => {
      counter.value--
    }
    return {
      counter,
      increaseCounter,
      decreaseCounter
    }
  }
}
</script>
-->
<!-- <script>
export default {
  data() {
    return {
      counter: 0
    }
  },
  methods: {
    increaseCounter() {
      this.counter++
    },
    decreaseCounter() {
      this.counter--
    }
  }
}
</script>
-->
<style scoped>
.home {
  margin-top: 20px;
}
.counter {
  display: flex;
  margin-top: 5px;
}
.button-container{
  display: flex;
}

.triangle-button {
  clip-path: polygon(75% 0%, 100% 50%, 75% 100%, 0% 100%, 25% 50%, 0% 0%);
  background: green;
  height: 60px;
  width: 130px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  padding-left: 10px;
}
.triangle-button:nth-child(n + 2) {
  margin-left: -32px;
}
.triangle-button:hover{
  background-color: yellow;
}
</style>
