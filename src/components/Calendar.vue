<template>
  <div
    class="container h-screen m-auto px-2 md:px-20 lg:px-40 flex flex-col justify-center transition duration-300"
    :class="{'bg-gray-800 text-white border-white' : dark,'bg-blue-100 text-black ' : !dark}"
  >
    <div class="flex flex-row justify-center">
      <SelectItem
        class="m-4"
        :items="months"
        :selectedItem="selectedMonth"
        @onItemChanged="onMonthChanged"
        :dark="dark"
      />
      <SelectItem
        class="m-4"
        :items="years"
        :selectedItem="selectedYear"
        @onItemChanged="onYearChanged"
        :dark="dark"
      />

      <button
        class="m-4 p-2 shadow-md"
        :class="{'bg-black text-white hover:bg-gray-600' : dark,'bg-blue-100 text-black  hover:bg-blue-200 ' : !dark}"
        @click="dark = !dark"
      >Make it {{dark ?"light" : "dark"}}</button>
    </div>
    <div
      class="grid grid-cols-7 text-xs text-center py-4 border-b-2 "
      :class="{'bg-black border-gray-600' : dark,'bg-blue-300 border-blue-600' : !dark}"
    >
      <div v-for="day in daysInWeek" :key="day">
        <span class="hidden sm:block">{{day}}</span>
        <span class="sm:hidden">{{day.substring(0,3)}}</span>
      </div>
    </div>

    <div
      class="grid grid-cols-7 text-center transition-all duration-300 ease-in-out"
      :class="{'bg-gray-700 ' : dark,' bg-blue-200 ' : !dark}"
    >
      <div
        v-for="item in noOfBlankBox"
        :key="'blank'+item"
      ></div>

      <div
        class="p-3 md:p-6 transition-all duration-300 ease-in-out"
        :class="{' hover:bg-gray-400 hover:text-black' : dark,'  hover:bg-blue-600 hover:text-white ' : !dark}"
        v-for="day in daysInMonth"
        :key="day"
      >{{day}}</div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

import SelectItem from "./SelectItem";

export default {
  name: "Calendar",
  components: { SelectItem },
  data() {
    return {
      daysInWeek: [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday",
      ],

      months: moment.months(),
      selectedMonth: moment().format("MMMM"),

      selectedYear: moment().year(),
      years: Array(100)
        .fill(1)
        .map((x, y) => 2000 + y),

      dark: false,
    };
  },
  computed: {
    selectedMonthInt() {
      return parseInt(moment().month(this.selectedMonth).format("M"));
    },
    daysInMonth() {
      return moment(
        `${this.selectedYear}-${this.selectedMonthInt}`
      ).daysInMonth();
    },
    noOfBlankBox() {
      return (
        moment(
          `${this.selectedYear}-${this.selectedMonthInt}-01`
        ).isoWeekday() - 1
      );
    },
  },
  methods: {
    onMonthChanged(data) {
      this.selectedMonth = data;
    },
    onYearChanged(data) {
      this.selectedYear = data;
    },
  },
};
</script>

<style>
</style>
