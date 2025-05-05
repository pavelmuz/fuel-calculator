<template>
  <div class="container">
    <n-flex vertical>
      <n-flex>
        <n-button @click="lengthTime = true">Время</n-button>
        <n-button @click="lengthTime = false">Круги</n-button>
      </n-flex>
      <p v-if="lengthTime">Время гонки</p>
      <p v-if="!lengthTime">Количество кругов</p>
      <n-input-number v-model:value="raceLength" :placeholder="lengthTime ? 'Минут' : 'Кругов'" />
      <p>Время круга</p>
      <n-flex>
        <n-input-number v-model:value="minutes" placeholder="Мин" />
        <n-input-number v-model:value="seconds" placeholder="Сек" />
        <n-input-number v-model:value="milliseconds" placeholder="Миллисек" />
      </n-flex>
      <p>Расход топлива</p>
      <n-input-number v-model:value="fuelPerLap" />
      <n-flex>
        <n-button @click="calcFuel">Рассчитать</n-button>
        <n-button @click="clearResults">Очистить</n-button>
      </n-flex>
      <n-flex>
        <p>Необходимо топлива:</p>
        <p>{{ fuelNeeded }}</p>
      </n-flex>
    </n-flex>
  </div>
</template>

<script setup>
import { NButton, NFlex, NInputNumber } from 'naive-ui'
import { ref } from 'vue'

const lengthTime = ref(true)
const raceLength = ref(null)
const fuelPerLap = ref(0)
const fuelNeeded = ref(0)
const minutes = ref(null)
const seconds = ref(null)
const milliseconds = ref(null)

function calcFuel() {
  if (lengthTime.value) {
    let lapTime = minutes.value * 60 + seconds.value + milliseconds.value / 1000
    fuelNeeded.value = ((raceLength.value * 60) / lapTime) * fuelPerLap.value
  } else {
    fuelNeeded.value = raceLength.value * fuelPerLap.value
  }
}

function clearResults() {
  raceLength.value = null
  fuelPerLap.value = 0
  raceLength.value = null
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
}
</style>
