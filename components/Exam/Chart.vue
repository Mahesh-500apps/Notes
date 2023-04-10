<template>
  <h2>Bar Chart</h2>
  <div style="max-width: 600px">
    <vue3-chart-js v-bind="{ ...barChart }" />
  </div>
</template>

<script setup lang="ts">
import Vue3ChartJs from "@j-t-mcc/vue3-chartjs";
interface Question {
  contacts: Array;
}
const props = withDefaults(defineProps<Question>(), {
  contacts: [],
});
const barChart = {
  type: "bar",
  options: {
    min: 0,
    max: 100,
    responsive: true,
    plugins: {
      legend: {
        position: "top",
      },
    },
    scales: {
      y: {
        min: 0,
        max: 100,
        ticks: {
          callback: function (value) {
            return `${value}%`;
          },
        },
      },
    },
  },
  data: {
    labels: props.contacts.map((contact: object) => {
      // Changing the edited tag
      return contact.name;
    }),
    datasets: [
      {
        label: "Age",
        backgroundColor: ["#2ecc71", "#e67e22", "#9b59b6", "#bdc3c7"],
        data: props.contacts.map((contact: object) => {
          // Changing the edited tag
          console.log(contact.age);
          return contact.age;
        }),
      },
    ],
  },
};
</script>
