<template>
  <div class="container">
    <n-flex vertical>
      <n-flex class="select-buttons">
        <n-button
          @click="lengthTime = true"
          class="btn"
          size="large"
          :color="lengthTime ? '#015551' : '#57B4BA'"
          :bordered="true"
          >Время</n-button
        >
        <n-button
          @click="lengthTime = false"
          class="btn"
          size="large"
          :color="lengthTime ? '#57B4BA' : '#015551'"
          >Круги</n-button
        >
      </n-flex>
      <p v-if="lengthTime">Время гонки</p>
      <p v-if="!lengthTime">Количество кругов</p>
      <n-input-number v-model:value="raceLength" :placeholder="lengthTime ? 'Минут' : 'Кругов'" />
      <p>Время круга</p>
      <n-flex>
        <n-input-number
          v-model:value="minutes"
          class="laptime"
          placeholder="Мин"
          :show-button="false"
        />
        <n-input-number
          v-model:value="seconds"
          class="laptime"
          placeholder="Сек"
          :max="59"
          :show-button="false"
        />
        <n-input-number
          v-model:value="milliseconds"
          class="laptime"
          placeholder="Мс"
          :max="999"
          :show-button="false"
        />
      </n-flex>
      <p>Расход топлива</p>
      <n-input-number v-model:value="fuelPerLap" />
      <n-flex align="center">
        <n-switch v-model:value="pitStop" />
        <p>Гонка с пит-стопом</p>
      </n-flex>
      <div v-if="pitStop">
        <p>Объем бака</p>
        <n-input-number v-model:value="tankCapacity" />
      </div>
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
import { NButton, NFlex, NInputNumber, NSwitch } from 'naive-ui'
import { ref } from 'vue'

const lengthTime = ref(true)
const raceLength = ref(null)
const fuelPerLap = ref(0)
const fuelNeeded = ref(0)
const minutes = ref(null)
const seconds = ref(null)
const milliseconds = ref(null)
const tankCapacity = ref(0)
const pitStop = ref(false)

function calcFuel() {
  if (lengthTime.value) {
    let lapTime = minutes.value * 60 + seconds.value + milliseconds.value / 1000
    let fuel = ((raceLength.value * 60) / lapTime) * fuelPerLap.value
    fuelNeeded.value = Math.ceil(fuel)
  } else {
    let fuel = raceLength.value * fuelPerLap.value
    fuelNeeded.value = Math.ceil(fuel)
  }
}

function clearResults() {
  raceLength.value = null
  fuelPerLap.value = 0
  raceLength.value = null
}
</script>

<style scoped>
p {
  font-size: 15px;
}
.container {
  display: flex;
  justify-content: center;
  margin: 20px;
}

.select-buttons {
  margin-left: auto;
  margin-right: auto;
}

.btn {
  width: 160px;
  border-radius: 6px;
}

.laptime {
  margin-left: auto;
  margin-right: auto;
  max-width: 100px;
}
</style>
