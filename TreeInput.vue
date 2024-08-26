<template>
  <div class="tree-input-container">
    <div
      ref="input"
      contenteditable="true"
      type="text"
      class="tree-input"
      placeholder="Select an area"
      @change="track()"
      @input="track(), search()"
      @click="handleInputClick"
    >
      {{ output }}
    </div>
    <span class="floating-label" :class="{ float: inputClicked || output }">{{
      label
    }}</span>
    <span v-if="output.length" class="close-icon" @click="handleClear"
      >&#11199;</span
    >
    <div class="list" v-if="inputClicked">
      <div class="parent" :class="{'parent-highlight': !parent.open}" v-for="parent in parents" :key="parent.id">
        <label @click="selectOutput(parent)" for=""
          ><span
            class="arrow"
            v-if="parent.hasChild"
            @click="parentArrowClicked(parent.id)"
            >{{ parent.open ? "&#11167;" : "&#11166;" }}</span
          >
          {{ parent.name[lang] }}
        </label>
        <div class="children" v-if="parent.open">
          <div class="child" v-for="area in parent.areas" :key="area.id">
            <label @click="selectOutput(area)" for="">{{ area.name[lang] }}</label>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
  
  <script setup>
import { onMounted, ref } from "vue";

const props = defineProps({
  mainList: {
    type: Array,
    requried: true,
  },
  lang: String
});

const emit = defineEmits(["selectedObject"]);

let mainList = props.mainList;
let inputClicked = ref(false);
const input = ref(null);
let output = ref("");
const label = ref(output.value.length ? "area" : "Select An Area");
const handleInputClick = () => {
  inputClicked.value = !inputClicked.value;
};
const search = (endpoint) => {
  parents.value = mainList.filter((parent) => {
    let childMatch;
    if (parent.hasChild) {
      childMatch = parent.areas.filter((area) => {
        if (area.name[props.lang].toLowerCase().includes(output.value.toLowerCase())) {
          return true;
        }
      });
    }
    return (
      parent.name[props.lang].toLowerCase().includes(output.value.toLowerCase()) ||
      childMatch.length
    );
  });
};
const track = () => {
  output.value = input.value.textContent;
  output.value.length == 0
    ? openAndCloseParents("closed")
    : openAndCloseParents("open");
};
const selectOutput = (option) => {
  output.value = option.name[props.lang];
  emit("selectedObject", option);
};

const handleClear = () => {
  output.value = "";
  parents.value = mainList;
  openAndCloseParents("closed");
};

const parents = ref(mainList);
const openAndCloseParents = (state) => {
  const states = {
    open: true,
    closed: false,
  };
  mainList.forEach((parent) => {
    parent.open = states[state];
  });
};

onMounted(() => {
  openAndCloseParents("closed");
});

const parentArrowClicked = (parentId) => {
  const parent = parents.value.find((parent) => parent.id == parentId);
  parent.open = !parent.open;
};
</script>
  
  <style lang="scss" scoped>
$font-color: #000;
$background-color: white;
$highlight-color: purple;
$background-highlight: rgb(237, 204, 237);
.tree-input-container {
  cursor: pointer;
  position: relative;
  .tree-input {
    box-sizing: border-box;
    border-radius: 12px;
    height: 50px;
    padding: 0.75rem 1.5rem;
    position: relative;
    z-index: 2;
    border: 1px solid gray;
    width: 100%;
    &:focus, &:hover{
        outline-color: $highlight-color;
        border-color: $highlight-color;
    }
  }
  .floating-label {
    color: #ddd;
    position: absolute;
    top: 16px;
    left: 25px;
    z-index: 3;
    transition: all 0.2s ease-in;
  }
  .float {
    font-size: 8px;
    color: $font-color;
    background-color: $background-color;
    top: -4px;
    left: 16px;
  }
  .list {
    position: absolute;
    padding: 16px 8px;
    background-color: $background-color;
    box-shadow: 0 4px 14px 0 rgba(94, 86, 105, 0.14);
    max-height: 304px;
    color: $font-color;
    width: 90%;
    left: 0;
    top: 40px;
    z-index: 3;
    border-radius: 5px;
    .child, .parent{
        padding: 2px 6px;
    }
    .parent-highlight{
        position: relative;
        z-index: 2;
        &::before{
        content: "";
        background-color: $background-highlight;
        position: absolute;
        width: 100%;
        height: 18px;
        border-radius: 4px;
        z-index: -1;
        display: none;
    }
    &:hover{
        &::before{
            display: block;
        }
    }
    }


     .child:hover{
        background-color: $background-highlight;
        border-radius: 4px;
    }
    .children {
      padding-left: 10px;
    }
  }
  label,
  .list span {
    cursor: pointer;
  }
  .close-icon {
    position: absolute;
    top: 14px;
    right: 10px;
    z-index: 3;
  }
  .arrow{
    font-size: 8px;
  }
}
</style>