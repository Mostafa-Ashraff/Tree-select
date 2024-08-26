<template>
  <TreeInput :mainList="listFromApi" @selected-object="SelectObjFromComp"/>
</template>

<script setup>
import { ref } from "vue";
import TreeInput from "./TreeInput.vue";
const listFromApi = ref([
  {
    id: 1,
    name: {
      en: "mahra",
      ar: "الجهراء",
    },
    parentId: null,
    hasChild: true,
    areas: [
      {
        id: 22,
        name: {
          en: "Al Naeem ",
          ar: "النعيم",
        },
        parentId: 1,
        hasChild: false,
      },
      {
        id: 21,
        name: {
          en: "Al mlama",
          ar: "النعيم",
        },
        parentId: 1,
        hasChild: false,
      },
    ],
  },
  {
    id: 2,
    name: {
      en: "Jahra",
      ar: "الجهراء",
    },
    parentId: null,
    hasChild: true,
    areas: [
      {
        id: 20,
        name: {
          en: "opa ",
          ar: "النعيم",
        },
        parentId: 1,
        hasChild: false,
      },
      {
        id: 19,
        name: {
          en: "lesa",
          ar: "النعيم",
        },
        parentId: 1,
        hasChild: false,
      },
    ],
  },
  {
    id: 3,
    name: {
      en: "nahra",
      ar: "الجهراء",
    },
    parentId: null,
    hasChild: true,
    areas: [
      {
        id: 10,
        name: {
          en: "opa ",
          ar: "النعيم",
        },
        parentId: 1,
        hasChild: false,
      },
      {
        id: 11,
        name: {
          en: "lesa",
          ar: "النعيم",
        },
        parentId: 1,
        hasChild: false,
      },
    ],
  },
]);
const SelectObjFromComp = (object)=>{
  console.log(object)
}
</script>

<style lang="scss" scoped>
</style>