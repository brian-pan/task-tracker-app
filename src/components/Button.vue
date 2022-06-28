<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
  <!-- instead of using shortcut, full sentences are: -->
  <!-- v-on:click="onClick()" -->
  <!-- v-bind:style="{background: color}" -->
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
  methods: {
    onClick() {
      console.log("click");
    },
  },
};
</script>
