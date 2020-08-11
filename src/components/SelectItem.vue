<template>
  <select  :value="selectedItem" @change="onChange" class="p-2 shadow-md" :class="{'bg-black text-white border-white  hover:bg-gray-600' : dark,'bg-blue-100 text-black  hover:bg-blue-200' : !dark}">
    <option v-for="item in items" :key="item" :value="item">{{item}}</option>
  </select>
</template>

<script>
// import moment from "moment";
export default {
  name: "SelectItem",
  data() {
    return {

    };
  },
  props:{
      items:Array,
      selectedItem:[String, Number],
      dark:Boolean
  },
  methods: {
    onChange(event) {
      console.log(event.target.value);
      this.$emit('onItemChanged',event.target.value)
    },
  },
};
</script>

<style>
</style>