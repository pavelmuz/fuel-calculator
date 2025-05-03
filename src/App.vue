<template>
  <div class="container">
    <n-flex vertical>
      <n-flex>
        <n-button @click="selectTime">Время</n-button>
        <n-button @click="selectLaps">Круги</n-button>
      </n-flex>
      <p v-if="lengthTime">Время гонки</p>
      <p v-if="lenghtLaps">Количество кругов</p>
      <n-input-number v-model:value="raceLength" />
      <p>Время круга</p>
      <n-flex>
        <n-input-number />
        <n-input-number />
        <n-input-number />
      </n-flex>
      <p>Расход топлива</p>
      <n-input-number v-model:value="fuelPerLap" />
      <n-flex>
        <n-button>Рассчитать</n-button>
        <n-button @click="clearResults">Очистить</n-button>
      </n-flex>
      <p>Необходимо топлива:</p>
    </n-flex>
  </div>
</template>

<script setup>
import { NButton, NFlex, NInputNumber } from 'naive-ui'
import { ref } from 'vue'

const lenghtLaps = ref(true)
const lengthTime = ref(false)
const raceLength = ref(0)
const fuelPerLap = ref(0)

function selectLaps() {
  lenghtLaps.value = true
  lengthTime.value = false
}

function selectTime() {
  lengthTime.value = true
  lenghtLaps.value = false
}

function clearResults() {
  raceLength.value = 0
  fuelPerLap.value = 0
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
}
</style>
