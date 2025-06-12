<script setup>
import {computed, onMounted, ref} from "vue";

const reportData = ref([
  {
    "month": "2023-01",
    "arr": 200000,
    "seats": 1012
  },
  {
    "month": "2023-02",
    "arr": 120000,
    "seats": 987
  },
  {
    "month": "2023-03",
    "arr": 240000,
    "seats": 1121
  },
  {
    "month": "2023-04",
    "arr": 160000,
    "seats": 1312
  },
  {
    "month": "2023-05",
    "arr": 210000,
    "seats": 1412
  },
  {
    "month": "2023-06",
    "arr": 170000,
    "seats": 2012
  }
])

const maxArr = computed(() => {
  return Math.max(...reportData.value.map(item => item.arr));
});

const totalArr = computed(() => {
  let temp = 0
  for (let key in reportData.value) {
    temp += reportData.value[key].arr
  }
  console.log(temp)

  return temp / 1000000
})

const totalSeats = computed(() => {
  let temp = 0
  for (let key in reportData.value) {
    temp += reportData.value[key].seats
  }
  console.log(temp)

  return temp
})

const fetchReport = async () => {
  const data = await fetch('https://startdeliver-mock-api.glitch.me/report')
  reportData.value = await data.json()
}

onMounted(() => {
  //fetchReport()
})

</script>

<template>
  <h2>Home</h2>
  <section class="stats-container">
    <section class="stats-section">
      <p class="gray title">ARR</p>
      <p class="stats-number">$ {{totalArr}} M</p>
    </section>

    <section class="stats-section">
      <p class="gray title">SEATS</p>
      <p class="stats-number">{{totalSeats}}</p>
    </section>

  </section>


  <section>
    <p class="gray title">NEW ARR PER MONTH</p>

    <div class="bar-chart">
      <div v-for="(block, index) in reportData" :key="index" class="bar-container">

        <div class="bar-wrapper">
          <div
              class="bar"
              :style="{ height: `${(block.arr / maxArr) * 100}%` }"
              :title="'$' + block.arr.toLocaleString()"
          >
          </div>
        </div>

        <div class="bar-label gray">{{ block.month }}</div>
      </div>
    </div>

  </section>
</template>

<style scoped>
.bar-chart {
  display: flex;
  height: 300px;
  align-items: flex-end;
  gap: 20px;
  margin-top: 20px;
}

.bar-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
  height: 100%;
}

.bar-label {
  margin-bottom: 8px;
  font-size: 0.9em;
  text-align: center;
}

.bar-wrapper {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  height: 100%;
  width: 100%;
}

.bar {
  background-color: #2250ff;
  width: 90%;
  min-width: 40px;
  border-radius: 4px 4px 0 0;
  transition: height 0.3s ease;
  position: relative;
  display: flex;
  justify-content: center;
}

.stats-container {
  display: flex;
  margin: 20px 0;

  .stats-section {
    flex: 1;

    .stats-number {
      font-size: 2em;
      font-weight: 600;
    }
  }

}

.gray {
  color: #a4aabd;
}

.title {
  font-size: 0.8em;
  font-weight: 600;
}
</style>