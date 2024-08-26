<template>
  <TreeInput :mainList="listFromApi" @selected-object="SelectObjFromComp" lang="ar"/>
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
      ar: "تتت",
    },
    parentId: null,
    hasChild: true,
    areas: [
      {
        id: 20,
        name: {
          en: "opa ",
          ar: "ةة",
        },
        parentId: 1,
        hasChild: false,
      },
      {
        id: 19,
        name: {
          en: "lesa",
          ar: "وو",
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
      ar: "الحم",
    },
    parentId: null,
    hasChild: true,
    areas: [
      {
        id: 10,
        name: {
          en: "opa ",
          ar: "اوبا",
        },
        parentId: 1,
        hasChild: false,
      },
      {
        id: 11,
        name: {
          en: "lesa",
          ar: "ليسا",
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