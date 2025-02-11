<template>
  <q-layout>
    <q-page-container>
      <q-page class="q-pa-md bg-dark text-white">
        <div class="action-btn-holder">
          <q-btn label="Print Response" class="btn-print" @click="printResult" />
          <q-btn label="Export to PDF" class="btn-export" @click="exportToPdf" />
        </div>

        <div class="container">
          <div class="left-side">
            <q-card class="propmt-card">
              <q-input
                class="additional-input"
                v-model="AdditionalPrompt"
                filled
                label="Additional Promt Base on the Result"
                type="textarea"
              ></q-input>
              <q-btn label="Send" class="btn-sendPromt" @click="sendPrompt" />
            </q-card>

            <q-section class="text-section">
              <div class="text-p">{{ outputMessageTitle }}</div>
              <div class="output-text text-p q-mt-md">{{ outputText }}</div>
            </q-section>
          </div>

          <div class="right-side">
            <q-card class="result-container">
              <q-card-section>
                <Bar :data="chartData" :options="chartOptions" class="result-chart" />
              </q-card-section>

              <q-card-section>
                <div class="text-p">{{ outputMessageTitle }}</div>
                <div class="output-text text-p q-mt-md">{{ outputText }}</div>
              </q-card-section>
            </q-card>
          </div>
        </div>

        <div class="row q-mt-md q-col-gutter-sm">
          <q-btn
            v-for="btn in buttons"
            :key="btn.label"
            :label="btn.label"
            :color="btn.color"
            class="query-btn"
            @click="handleButtonClick(btn.label)"
          />
        </div>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { Chart, registerables } from 'chart.js'
import { Bar } from 'vue-chartjs'

// Register Chart.js components
Chart.register(...registerables)

const AdditionalPrompt = ref('')

const chartData = ref({
  labels: ['Q1', 'Q2', 'Q3', 'Q4'],
  datasets: [
    {
      label: 'AHT Data',
      data: [10, 20, 30, 25],
      backgroundColor: ['#76f2c1', '#62e1b1', '#48c89d', '#36b089'],
    },
  ],
})

const chartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
})

const buttons = ref([
  { label: 'Generate the FCR for Supervisor 2', color: 'transparent' },
  { label: 'Generate Quarter View of AHT in Bar Graph', color: 'transparent' },
  { label: 'Generate Customer Satisfaction for Supervisor 1', color: 'transparent' },
  { label: 'Generate CRES for this month', color: 'transparent' },
  {
    label: 'Generate FCR per Supervisor for the previous month in Line Graph',
    color: 'transparent',
  },
])

const outputMessageTitle = ref('')
const outputText = ref('')

const sendPrompt = () => {
  outputMessageTitle.value = "Here's the quarter view of AHT in Bar Graph"
  outputText.value = 'Lorem Ipsum is simply dummy text of the printing and typesetting industry'
}
</script>

<style scope>
.action-btn-holder {
  width: 100%;
  background: transparent;
  display: flex;
  gap: 20px;
  justify-content: end;
  padding-right: 20px;
  margin-bottom: 10px;
}

.btn-print,
.btn-export {
  color: rgb(42, 221, 197);
  width: 200px;
}

.btn-export::before,
.btn-print::before {
  content: '';
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  height: 0.5px;
  background: #00ffea;
  box-shadow:
    0 0 1px #00ffea,
    0 0 1px #00ffea;
  transition: all 0.3s ease;
}

.btn-export::after,
.btn-print::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  height: 1px;
  background: #00ffea;
  box-shadow:
    0 0 1px #00ffea,
    0 0 10px #00ffea; /* Glow effect */
  transition: all 0.3s ease;
}

.container {
  display: flex;
  gap: 40px;
}

.left-side {
  width: 65%;
  height: 100vh;
  background: rgb(12, 11, 20);
  box-shadow: 10px 10px 20px rgba(0, 0, 0, 0.5);
  border-radius: 20px;
  padding: 20px 20px 0 20px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.propmt-card {
  background: transparent;
  border: 1px solid rgb(42, 221, 197);
  color: rgb(42, 221, 197);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.additional-input {
  transition: none;
  width: 100%;
}

.btn-sendPromt {
  background: rgb(4, 112, 98);
  width: 100px;
  border-radius: 10px;
  color: white;
  margin: 10px 10px 10px auto;
}

.output-text {
  text-align: justify;
}

.right-side {
  background: rgb(12, 11, 20);
  width: 35%;
  display: flex;
  flex-direction: column;
  box-shadow: 10px 10px 20px rgba(0, 0, 0, 0.5);
}

.result-container {
  background: transparent;
}

.result-chart {
  height: 250px;
  background: black;
}
</style>
