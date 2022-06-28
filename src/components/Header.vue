<template>
  <header>
    <h1>Task Tracker</h1>
  </header>
</template>

<script>
export default {
  name: "Header",
  components: {},
};
</script>

<style scoped>
/* scoped means style only apply to this component */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
